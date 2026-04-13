# OAuth 2.1

Both the **Retrieval API** and the **Audit API** use OAuth 2.1 for authentication. There are two kinds of callers:

* **Browsers** — use the `kai_auth` HttpOnly cookie set by `https://auth.kai-studio.ai` after login. Transparent to your application code.
* **MCP clients & custom integrations** — use the full OAuth 2.1 Authorization Code + PKCE flow with Dynamic Client Registration. This page documents that flow in detail.

### Authorization Server

All OAuth endpoints live on **`https://auth-api.kai-studio.ai`**, with a discovery document mirrored on each API:

* `GET https://api-retrieval.kai-studio.ai/.well-known/oauth-authorization-server`
* `GET https://api-audit.kai-studio.ai/.well-known/oauth-authorization-server`

Both discovery documents return identical metadata pointing to the same Authorization Server. A token issued via either surface is accepted on both APIs (same signing key).

### Flow for MCP clients & custom integrations

#### 1. Discover

Fetch the Authorization Server metadata from the API you want to use:

```http
GET https://api-retrieval.kai-studio.ai/.well-known/oauth-authorization-server
```

Response:

```json
{
  "issuer": "https://auth-api.kai-studio.ai",
  "authorization_endpoint": "https://auth-api.kai-studio.ai/auth/oauth/authorize",
  "token_endpoint": "https://auth-api.kai-studio.ai/auth/oauth/token",
  "registration_endpoint": "https://auth-api.kai-studio.ai/auth/oauth/register",
  "revocation_endpoint": "https://auth-api.kai-studio.ai/auth/oauth/revoke",
  "response_types_supported": ["code"],
  "grant_types_supported": ["authorization_code", "refresh_token"],
  "code_challenge_methods_supported": ["S256"],
  "token_endpoint_auth_methods_supported": ["client_secret_basic", "client_secret_post"],
  "scopes_supported": ["mcp"]
}
```

#### 2. Register (Dynamic Client Registration — RFC 7591)

Register your client to obtain a `client_id` and `client_secret`:

```http
POST https://auth-api.kai-studio.ai/auth/oauth/register
Content-Type: application/json

{
  "client_name": "My MCP Client",
  "redirect_uris": ["https://my-app.example.com/callback"],
  "grant_types": ["authorization_code", "refresh_token"],
  "token_endpoint_auth_method": "client_secret_post"
}
```

Response (`201 Created`):

```json
{
  "client_id": "<generated-uuid>",
  "client_secret": "<generated-secret>",
  "client_name": "My MCP Client",
  "redirect_uris": ["https://my-app.example.com/callback"],
  "grant_types": ["authorization_code", "refresh_token"],
  "token_endpoint_auth_method": "client_secret_post"
}
```

{% hint style="info" %}
**Store `client_secret` securely.** It is returned only once and cannot be retrieved later.
{% endhint %}

Registration is rate-limited (5 requests per minute per IP). In production, localhost redirect URIs are rejected.

#### 3. Authorize (Authorization Code + PKCE)

Generate a PKCE code verifier and challenge:

1. Create a random `code_verifier` (43-128 characters, `[A-Za-z0-9\-._~]`).
2. Compute `code_challenge = BASE64URL(SHA256(code_verifier))`.
3. Generate a random `state` parameter for CSRF protection.

Redirect the user's browser to:

```
https://auth-api.kai-studio.ai/auth/oauth/authorize
  ?response_type=code
  &client_id=<client_id>
  &redirect_uri=https://my-app.example.com/callback
  &code_challenge=<code_challenge>
  &code_challenge_method=S256
  &state=<state>
  &scope=mcp
```

If the user is not logged in, they are redirected to the KAI login page (`auth.kai-studio.ai`). After authentication, the Authorization Server issues an authorization code and redirects back:

```
https://my-app.example.com/callback?code=<authorization_code>&state=<state>
```

Verify that `state` matches the value you sent. Authorization codes expire after **10 minutes** and are single-use.

#### 4. Exchange code for tokens

```http
POST https://auth-api.kai-studio.ai/auth/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code
&code=<authorization_code>
&redirect_uri=https://my-app.example.com/callback
&client_id=<client_id>
&client_secret=<client_secret>
&code_verifier=<code_verifier>
```

Response:

```json
{
  "access_token": "<jwt>",
  "refresh_token": "<opaque-token>",
  "token_type": "Bearer",
  "expires_in": 900
}
```

* **Access token**: JWT, valid for **15 minutes** (`expires_in: 900`). Signed with HS256.
* **Refresh token**: opaque, valid for **7 days**. Rotated on every use (see below).

Client authentication supports both `client_secret_post` (credentials in form body) and `client_secret_basic` (HTTP Basic `Authorization` header).

#### 5. Call the API

Include the access token as a Bearer token:

```http
POST https://api-retrieval.kai-studio.ai/retrieval/semantic-nodes/search
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "query": "What are the safety requirements?",
  "instance_id": "<instance-id>"
}
```

The same token works on both `api-retrieval.kai-studio.ai` and `api-audit.kai-studio.ai`.

#### 6. Refresh

When the access token expires, use the refresh token to obtain a new pair:

```http
POST https://auth-api.kai-studio.ai/auth/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token
&refresh_token=<refresh_token>
&client_id=<client_id>
&client_secret=<client_secret>
```

Response: same shape as step 4, with a **new** access token and a **new** refresh token.

{% hint style="warning" %}
**Forced rotation.** The old refresh token is revoked immediately upon use. You must store the new refresh token from each response. If a revoked refresh token is presented again, the entire token chain is revoked and the user must re-authorize — this is a security measure against token theft.
{% endhint %}

#### 7. Revoke (optional, on logout)

```http
POST https://auth-api.kai-studio.ai/auth/oauth/revoke
Content-Type: application/x-www-form-urlencoded

token=<refresh_token>
```

Returns `200 OK` regardless of whether the token was valid (per RFC 7009).

### Flow for browsers

Browser-based applications (such as `audit-ui`) do not use the OAuth flow described above. Instead:

1. The application redirects unauthenticated users to `https://auth.kai-studio.ai/login`.
2. After login, the auth service sets an HttpOnly cookie named `kai_auth` on the `.kai-studio.ai` domain.
3. The cookie contains a JWT (15-minute lifetime) and is sent automatically with every request to `*.kai-studio.ai`.
4. A sliding-window refresh mechanism renews the cookie server-side when the JWT passes 50% of its lifetime.

No additional integration is required on the application side — the cookie is transparent.

**Supported SSO providers (today):** Microsoft multi-tenant (Azure AD / OIDC). Users must have a pre-existing account in KAI; SSO matches by email.

### Why not a simple API key for end-users?

The KAI Instance API uses static API keys because it serves machine-to-machine pipelines with no user identity. For human users and LLM agents acting on behalf of humans, OAuth 2.1 provides what API keys cannot: per-user identity (enabling group-aware access control), token expiration and revocation (limiting blast radius if a credential leaks), and audit trails (knowing which user accessed which instance and when).

### MCP-specific notes

* Both `api-audit.kai-studio.ai` and `api-retrieval.kai-studio.ai` publish their own `/.well-known/oauth-authorization-server` document, but both point to the **same** Authorization Server (`auth-api.kai-studio.ai`). You only need to register your client once.
* Access tokens are accepted on both APIs without re-registration or re-authorization.
* MCP clients should transparently refresh access tokens every \~15 minutes. Claude Desktop, Cursor, and Le Chat handle this automatically when configured with a KAI MCP server URL.
* The MCP endpoints (`/mcp` on each API) use Bearer token authentication, not cookies. Cookie auth is reserved for browser-based applications.
