---
description: >-
  This page walks through installing the KAI MCP servers (Retrieval + Audit
  BETA) into the major MCP-compatible clients.
---

# Connecting a client

### Cursor (one-click)

[**⚡ Install KAI Retrieval**](cursor://anysphere.cursor-deeplink/mcp/install?name=KAI%20Retrieval\&config=eyJ1cmwiOiJodHRwczovL2FwaS1yZXRyaWV2YWwua2FpLXN0dWRpby5haS9tY3AifQ==)\
\
[**⚡ Install KAI Audit (BETA)**](cursor://anysphere.cursor-deeplink/mcp/install?name=KAI%20Audit%20%28BETA%29\&config=eyJ1cmwiOiJodHRwczovL2FwaS1hdWRpdC5rYWktc3R1ZGlvLmFpL21jcCJ9)

Manual fallback — add to your Cursor MCP config (`~/.cursor/mcp.json` or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "kai-retrieval": {
      "url": "https://api-retrieval.kai-studio.ai/mcp"
    },
    "kai-audit": {
      "url": "https://api-audit.kai-studio.ai/mcp"
    }
  }
}
```

> **Note:** on some Linux distributions (notably Debian), `cursor://` deep-links may fail to open the app. Use the manual config if the buttons don't work.

### Claude Desktop (manual)

Claude Desktop does not expose a public deep-link scheme for MCP installation as of 2026-04-13.

**Recommended (web UI — Custom Connectors):**

1. Open [claude.ai](https://claude.ai) and sign in (requires Pro, Max, Team, or Enterprise plan).
2. Click your profile icon > **Settings** > **Connectors**.
3. Click **+** then **Add custom connector**.
4. Add two connectors:
   * URL: `https://api-retrieval.kai-studio.ai/mcp`
   * URL: `https://api-audit.kai-studio.ai/mcp`
5. Complete the OAuth flow in the browser popup for each.

{% hint style="info" %}
Remote MCP servers must be added through the web UI Custom Connectors, not via `claude_desktop_config.json`. The config file is intended for local stdio servers only.
{% endhint %}

### Mistral Le Chat (manual)

Le Chat does not expose a public deep-link scheme. Add each connector through the web UI:

1. Open [chat.mistral.ai](https://chat.mistral.ai) and sign in.
2. Click the **toggle panel button** (sidebar).
3. Expand **Intelligence** > click **Connectors**.
4. Click **+ Add Connector** > select the **Custom MCP Connector** tab.
5. Fill in the form:

| Field                 | KAI Retrieval                             | KAI Audit (BETA)                      |
| --------------------- | ----------------------------------------- | ------------------------------------- |
| **Connector name**    | `kai-retrieval`                           | `kai-audit`                           |
| **Connection server** | `https://api-retrieval.kai-studio.ai/mcp` | `https://api-audit.kai-studio.ai/mcp` |
| **Description**       | KAI document retrieval                    | KAI document audit (BETA)             |
| **Authentication**    | OAuth 2.1 (auto-detected)                 | OAuth 2.1 (auto-detected)             |

6. Click **Connect** and complete the OAuth authentication flow.
7. In any chat, click the **Tools** button (four-squares icon) and enable the connector.

> **Note:** Adding Custom Connectors may require Admin privileges on the Le Chat account.

### Other MCP-compatible clients

Manual configuration:

* **MCP server URLs:**
  * Retrieval: `https://api-retrieval.kai-studio.ai/mcp`
  * Audit (BETA): `https://api-audit.kai-studio.ai/mcp`
* **OAuth discovery:** `/.well-known/oauth-authorization-server` on either URL (both point to `auth-api.kai-studio.ai`).
* **Transport:** Streamable HTTP.

See OAuth flow for MCP (detailed) if your client requires manual OAuth setup.
