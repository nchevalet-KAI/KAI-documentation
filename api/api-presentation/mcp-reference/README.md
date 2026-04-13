---
description: What is MCP & why we expose it
---

# MCP Reference

The [**Model Context Protocol (MCP)**](https://modelcontextprotocol.io/) is an open standard, maintained by Anthropic, that lets a host LLM discover and invoke **tools** exposed by third-party servers — with the end-user's own credentials.

### Why KAI exposes MCP

We want your users' LLM clients — Claude Desktop, Cursor, Mistral Le Chat, or any MCP-compatible agent — to be able to answer questions and run workflows on top of KAI knowledge, without us dictating a RAG strategy or maintaining chat state server-side.

Instead of a single imposed `/search` endpoint, we expose **primitives** (list instances, search semantic nodes, fetch documents, drive audits) as MCP tools. The host LLM does the orchestration. The user's OAuth 2.1 credentials carry their group-based permissions, their visibility rules, and their per-instance instructions into every tool call.

This is why `/search` and `/conversation` were removed — see Why MCP for the full story.

### Retrieval MCP vs Audit MCP

| Aspect          | Retrieval MCP                             | Audit MCP                                    |
| --------------- | ----------------------------------------- | -------------------------------------------- |
| Status          | ✅ Stable                                  | 🧪 **BETA**                                  |
| URL             | `https://api-retrieval.kai-studio.ai/mcp` | `https://api-audit.kai-studio.ai/mcp`        |
| Tool count      | 5                                         | 40                                           |
| Shape           | Read-oriented (search, fetch)             | Workflow-oriented (state machine, mutations) |
| Recommended use | Production RAG/agent usage                | Exploration + light integration              |

Both servers share the same OAuth 2.1 Authorization Server (`auth-api.kai-studio.ai`) — a token obtained from one is accepted on the other.
