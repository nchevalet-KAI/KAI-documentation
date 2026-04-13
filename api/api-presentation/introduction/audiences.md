---
description: who uses what
---

# Audiences

| Surface                                           | Who uses it                                                                                                                                  | MCP?                | Why                                                                                                                        |
| ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **KAI Instance API** (`api.kai-studio.ai`)        | Integrators building machine-to-machine pipelines (ingestion, indexation, custom backoffice)                                                 | ❌                   | Low-level, per-instance, deterministic. No human user, no group-aware multi-tenant, not suited to generic LLM consumption. |
| **Audit API** (`api-audit.kai-studio.ai`)         | 1) `audit-ui` (browser, cookie auth) — 2) MCP clients (Claude Desktop/Code, Cursor, Le Chat) driving an audit workflow from an LLM           | ✅ 40 tools **BETA** | Multi-step workflow → LLM can orchestrate via MCP. Human user delegating to an agent → OAuth 2.1.                          |
| **Retrieval API** (`api-retrieval.kai-studio.ai`) | 1) MCP clients (canonical use case — replacement of `/search` and `/conversation`) — 2) Custom integrations requiring user-level permissions | ✅ 5 tools (stable)  | Textbook MCP use case: expose knowledge primitives to a host LLM that orchestrates search and conversation itself.         |

### When to use which

> **I want to ingest documents from my own system into KAI.** → KAI Instance API → Orchestrator.

> **I want to let Claude / Cursor / Le Chat answer questions on top of my KAI knowledge.** → Retrieval API over MCP → MCP usage.

> **I want to automate document-audit workflows from an LLM.** → Audit API over MCP (BETA) → MCP usage.

> **I want my team to run audits in a browser.** → Use `audit-ui`, no API integration needed.
