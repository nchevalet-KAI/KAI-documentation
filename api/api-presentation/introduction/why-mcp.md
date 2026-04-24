---
description: the /search and /conversation removal
---

# Why MCP

Until recently, the KAI Instance API exposed two high-level endpoints:

* **`/search`** — performed server-side RAG: KAI decided the retrieval strategy, called an LLM internally, and returned a natural-language answer.
* **`/conversation`** — maintained chatbot state server-side across turns, wrapping `/search` in a multi-turn loop.

Both are **removed as of 2026-04-13**. Here is why, and what replaces them.

### The problem with server-side RAG

Server-side RAG imposed a single retrieval-and-generation strategy on every caller. If you were building an agent with Claude Desktop or Cursor, KAI's `/search` duplicated what the host LLM already does — retrieve context, reason over it, compose an answer — but with no way to control the retrieval parameters, the prompt, or the model. The `/conversation` endpoint went further by keeping chat history on the server, creating an awkward split where the client's LLM had one conversation context and KAI had another.

In an ecosystem where LLMs are the orchestrators, the right role for a knowledge platform is to expose **primitives** — list what instances exist, search semantic nodes, fetch documents — and let the client decide how to use them.

### The switch to MCP

The [Model Context Protocol](https://modelcontextprotocol.io/) (MCP) is an open standard for exposing tools to a host LLM. KAI now publishes its knowledge primitives as MCP tools on the **Retrieval API**, so any compatible client can orchestrate search and conversation natively.

Concrete mapping:

* `/search` is replaced by **Retrieval API — `semantic-nodes/search`**. The client LLM calls this tool to retrieve relevant nodes, then synthesises the answer itself with full control over the prompt and model.
* `/conversation` has no replacement endpoint. Conversation state is now handled entirely on the MCP client side (Claude Desktop, Cursor, Le Chat). The host LLM maintains its own context window across turns.

Authentication moves from static API keys (per-instance, no user identity) to **OAuth 2.1** (per-user, group-aware permissions). A single token grants access to every instance the user is entitled to — no more juggling one API key per instance.

### Why MCP on Audit

The audit workflow — surfacing conflicts across documents, recording expert answers, generating modification recommendations, closing resolved items — is a multi-step process that maps naturally to an LLM agent coordinating tools. The **Audit API** therefore exposes a **curated 19-tool subset** of its 40 REST endpoints as MCP tools, built around the **conflict-first workflow** (dashboard → list open conflicts → record answer → confirm applied → mark managed). Admin, stats, duplicates, user membership, and question-level writes stay REST-only for `audit-ui`.

The API contracts are stable, but the MCP response schemas may evolve. Instance creation / configuration and the audit-launch state machine (`INIT` through `RUNNING_PHASE`) are intentionally **not** on MCP — we recommend starting audits via the `audit-ui` browser interface and using MCP for exploring and resolving conflicts on an existing audit.

**Next:** Retrieval API overview | Audit API overview
