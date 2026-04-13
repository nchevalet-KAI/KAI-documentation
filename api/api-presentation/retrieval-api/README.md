# Retrieval API

The **Retrieval API** is the high-level, multi-tenant, user-authenticated path into KAI knowledge. It is the **replacement for the removed `/search` endpoint** and the primary way to expose a user's KAI instances to a host LLM via MCP.

### When to use

✅ **Right fit for:**

* Exposing KAI knowledge to an end-user's LLM client (Claude Desktop, Cursor, Le Chat, ...) — the canonical MCP use case.
* Custom client-side integrations that need user-level permissions, not just per-instance isolation.
* Any application where the caller is a human user with a KAI account.

🚫 **Not the right fit for:**

* Back-end indexation or ingestion pipelines → use the KAI Instance API.

### Key differences vs the Instance API

| Aspect               | Instance API                               | Retrieval API                           |
| -------------------- | ------------------------------------------ | --------------------------------------- |
| Auth model           | `instance_id` + `api_key`                  | OAuth 2.1 (user)                        |
| Scope per credential | One instance                               | All instances the user can access       |
| Permissions          | None (anyone with the key has full access) | Group-based RBAC, per-user instructions |
| MCP support          | ❌                                          | ✅ 5 tools, stable                       |

### Base URL & conventions

* **Base URL:** `https://api-retrieval.kai-studio.ai`
* **Auth:** Bearer JWT (MCP / custom integrations) or HttpOnly cookie `kai_auth` (browsers). See OAuth 2.1.
* **Methods:** all endpoints are `POST` with JSON body.
* **Response wrapper:** all successful responses are wrapped in `{"response": <payload>}`.
* **Errors:** standard HTTP status codes (401 for missing/invalid token, 403 for access denied to an instance, 404 for unknown resource).

### Endpoints

| Page           | Endpoints                             |
| -------------- | ------------------------------------- |
| Instances      | `list-available-instances`            |
| Documents      | `list`, `get-document`, `list-by-ids` |
| Semantic nodes | `search` — the `/search` replacement  |

### MCP

All endpoints are also exposed as MCP tools. See **MCP usage** for installation into Claude Desktop, Cursor, and Mistral Le Chat.
