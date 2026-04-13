# MCP usage (BETA)

{% hint style="warning" %}
**BETA.** All 40 Audit API endpoints are exposed as MCP tools, but tool schemas may evolve. Recommended for exploration only — do not rely on this for production-critical audit orchestration.
{% endhint %}

### Endpoint

* **MCP URL:** `https://api-audit.kai-studio.ai/mcp`
* **Transport:** Streamable HTTP, stateless.
* **Auth:** OAuth 2.1, discovered from `https://api-audit.kai-studio.ai/.well-known/oauth-authorization-server`. The same tokens work on the Retrieval API.

### What works well today

* Exploring the state of existing audits (list instances, check status, fetch duplicates / conflicts / questions).
* Reading stats and counters.
* Setting answers and marking items as managed (write operations on individual resources).
* Read-heavy workflows from a host LLM.

### What's rough

The audit-launch state machine (`INIT` → `ON_CHECKING_INDEXATION` → `CHECK_INDEXATION_DONE` → `LAUNCH_DUPLICATE_IDENTIFICATION` → `ON_DUPLICATE_IDENTIFICATION` → `DUPLICATE_IDENTIFICATION_DONE` → `RUNNING_PHASE`) is complex, with background tasks and step transitions. It is **not yet fully smooth via MCP** — some transitions depend on background workers that may surface async feedback not ideally represented as synchronous tool returns.

**Recommendation for BETA:** start an audit in `audit-ui` and let MCP clients explore and query it afterwards. Full end-to-end automation via MCP will become first-class in a future release.

### Installation per client

{% tabs %}
{% tab title="Cursor (one-click)" %}
[**⚡ Install KAI Audit (BETA) in Cursor**](cursor://anysphere.cursor-deeplink/mcp/install?name=KAI%20Audit%20%28BETA%29\&config=eyJ1cmwiOiJodHRwczovL2FwaS1hdWRpdC5rYWktc3R1ZGlvLmFpL21jcCJ9)

Manual fallback (add to Cursor's MCP config at `~/.cursor/mcp.json` or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "kai-audit": {
      "url": "https://api-audit.kai-studio.ai/mcp"
    }
  }
}
```

> **Note:** on some Linux distributions (notably Debian), `cursor://` deep-links may fail to open the app. If the button above does not work, use the manual config.
{% endtab %}

{% tab title="Claude Desktop (manual)" %}
Claude Desktop does not expose a public deep-link scheme for MCP installation as of 2026-04-13. Use the Custom Connectors web UI:

1. Open [claude.ai](https://claude.ai) and sign in (requires Pro, Max, Team, or Enterprise plan).
2. Click your profile icon > **Settings** > **Connectors**.
3. Click **+** then **Add custom connector**.
4. Enter the URL: `https://api-audit.kai-studio.ai/mcp`
5. Complete the OAuth flow in the browser popup.

{% hint style="info" %}
Remote MCP servers must be added through the web UI Custom Connectors, not via `claude_desktop_config.json`. The config file is intended for local stdio servers only.
{% endhint %}
{% endtab %}

{% tab title="Mistral Le Chat (manual)" %}
Le Chat does not expose a public deep-link scheme. Add the connector through the web UI:

1. Open [chat.mistral.ai](https://chat.mistral.ai) and sign in.
2. Click the **toggle panel button** (sidebar).
3. Expand **Intelligence** > click **Connectors**.
4. Click **+ Add Connector** > select the **Custom MCP Connector** tab.
5. Fill in the form:
   * **Connector name:** `kai-audit`
   * **Connection server:** `https://api-audit.kai-studio.ai/mcp`
   * **Description:** KAI document audit (BETA)
   * **Authentication:** OAuth 2.1 (auto-detected)
6. Click **Connect** and complete the OAuth authentication flow.
7. In any chat, click the **Tools** button (four-squares icon) and enable the `kai-audit` connector.

> **Note:** Adding Custom Connectors may require Admin privileges on the Le Chat account.
{% endtab %}
{% endtabs %}

### First-connection flow

1. Your MCP client discovers OAuth via the discovery document at `/.well-known/oauth-authorization-server`.
2. It dynamically registers itself (DCR).
3. A browser window opens for user authentication (Microsoft SSO or local login).
4. Tokens are exchanged and stored by the client.
5. Subsequent tool calls are authenticated transparently; refresh tokens are rotated automatically.

See OAuth 2.1 for the full flow.
