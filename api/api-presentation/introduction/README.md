# Introduction

KAI exposes three distinct API surfaces, each tailored to a different class of consumer.

```mermaid
flowchart TB
    subgraph apis["API Surfaces"]
        direction LR
        instance["<b>KAI Instance API</b><br/><code>https://api.kai-studio.ai</code><br/>Orchestrator · Documents · Audit · Semantic Graph<br/><i>Auth: instance-id + api-key headers</i>"]
        retrieval["<b>Retrieval API</b><br/><code>https://api-retrieval.kai-studio.ai</code><br/>Instances · Documents · Semantic Nodes<br/><i>Auth: OAuth 2.1 (Bearer JWT)</i>"]
        audit["<b>Audit API</b><br/><code>https://api-audit.kai-studio.ai</code><br/>40 endpoints — full audit workflow<br/><i>Auth: OAuth 2.1 (Bearer JWT / cookie)</i>"]
    end

    pipelines["Integration pipelines<br/><i>Scripts, backoffice, ETL</i>"]
    mcp["MCP clients<br/><i>Claude Desktop · Cursor · Le Chat</i>"]
    auditui["audit-ui<br/><i>Browser</i>"]

    pipelines -->|"API key"| instance
    mcp -->|"OAuth 2.1 + MCP"| retrieval
    mcp -->|"OAuth 2.1 + MCP (BETA)"| audit
    auditui -->|"Cookie (kai_auth)"| audit
```

* **KAI Instance API** (`https://api.kai-studio.ai`) — low-level, machine-to-machine. Use it to build your own indexation pipelines or backoffice integrations.
* **Retrieval API** (`https://api-retrieval.kai-studio.ai`) — high-level, multi-tenant, group-aware. Primary path for exposing your KAI knowledge to a host LLM via MCP.
* **Audit API** (`https://api-audit.kai-studio.ai`) — drives the audit-ui workflow (browser) and, in BETA, lets an LLM coordinate an audit via MCP.

Continue to **Audiences — who uses what** to identify where your use case fits, and to **Why MCP** for the editorial context behind this split.
