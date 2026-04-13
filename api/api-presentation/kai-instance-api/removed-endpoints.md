# Removed endpoints

The following endpoints are **no longer available on the KAI Instance API** as of **2026-04-13**. They were removed as part of the shift toward MCP-based orchestration (see Why MCP).

### `/search`

**Removed.** Server-side RAG is no longer offered by KAI.

→ **Replacement:** Retrieval API — `POST /retrieval/semantic-nodes/search`. The new endpoint returns raw semantic nodes; your application (or your LLM over MCP) performs the final answer-composition.

### `/conversation`

**Removed.** KAI no longer maintains chatbot state server-side.

→ **Replacement:** conversation state is now handled **on the MCP client side** (Claude Desktop, Cursor, Le Chat, ...). Your host LLM maintains the history. See Why MCP for context.
