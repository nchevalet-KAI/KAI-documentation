---
description: >-
  The Retrieval API is available as an MCP server, exposing its 5 endpoints as
  tools for any MCP-compatible LLM client.
---

# MCP Usage

### Endpoint

* **MCP URL:** `https://api-retrieval.kai-studio.ai/mcp`
* **Transport:** Streamable HTTP, stateless (no server-side sessions).
* **Auth:** OAuth 2.1, discovered automatically from `https://api-retrieval.kai-studio.ai/.well-known/oauth-authorization-server`.

### Exposed tools

| Tool (`operation_id`)                          | Endpoint                                             | Description                                                     |
| ---------------------------------------------- | ---------------------------------------------------- | --------------------------------------------------------------- |
| `retrieval_instances_list_available_instances` | `POST /retrieval/instances/list-available-instances` | List the user's accessible instances with composed instructions |
| `retrieval_documents_list`                     | `POST /retrieval/documents/list`                     | Paginated list of documents in an instance                      |
| `retrieval_documents_get_document`             | `POST /retrieval/documents/get-document`             | Fetch the full content of one document                          |
| `retrieval_documents_list_by_ids`              | `POST /retrieval/documents/list-by-ids`              | Fetch multiple documents by ID in a single call                 |
| `retrieval_semantic_nodes_search`              | `POST /retrieval/semantic-nodes/search`              | Semantic search (replaces `/search`)                            |

### Installation per client

{% tabs %}
{% tab title="Cursor (one-click)" %}
[**⚡ Install KAI Retrieval in Cursor**](cursor://anysphere.cursor-deeplink/mcp/install?name=KAI%20Retrieval\&config=eyJ1cmwiOiJodHRwczovL2FwaS1yZXRyaWV2YWwua2FpLXN0dWRpby5haS9tY3AifQ==)

Manual fallback (add to Cursor's MCP config at `~/.cursor/mcp.json` or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "kai-retrieval": {
      "url": "https://api-retrieval.kai-studio.ai/mcp"
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
4. Enter the URL: `https://api-retrieval.kai-studio.ai/mcp`
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
   * **Connector name:** `kai-retrieval`
   * **Connection server:** `https://api-retrieval.kai-studio.ai/mcp`
   * **Description:** KAI document retrieval
   * **Authentication:** OAuth 2.1 (auto-detected)
6. Click **Connect** and complete the OAuth authentication flow.
7. In any chat, click the **Tools** button (four-squares icon) and enable the `kai-retrieval` connector.

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
