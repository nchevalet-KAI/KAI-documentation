# KAI Instance API

The **KAI Instance API** is the low-level, per-instance surface of the KAI platform. It exposes indexation control, document metadata, raw audit primitives, and semantic-graph exploration — all scoped to a single instance.

### When to use

✅ **Right fit for:**

* Custom document-ingestion pipelines pushing content into KAI.
* Third-party system synchronisation (CMS, S3 drop zones, DMS, ...).
* Internal backoffice integrations (reporting, admin tooling).
* Machine-to-machine automation where no human user is involved.

🚫 **Not the right fit for:**

* Exposing KAI knowledge to an end-user's LLM → use the Retrieval API over MCP.
* Driving the audit workflow with UI or from an agent → use the Audit API.

### Base URL & conventions

* **Base URL:** `https://api.kai-studio.ai` (single shared host — the instance targeted by a request is determined by the `instance-id` header).
* **Auth:** `instance-id` + `api-key` headers — see Instance API keys.
* **Format:** JSON request bodies, JSON responses.
* **Pagination:** where applicable, `offset` and `limit` query parameters (default `offset=0`, `limit=20` or `limit=50` depending on the endpoint).
* **Response wrapper:** all successful responses are wrapped in `{"response": <payload>}`.
* **Errors:** standard HTTP status codes (400 validation, 401 auth, 404 not found, 500 server error). Error bodies follow `{ "detail": "<message>" }`.

### Endpoint categories

| Category          | What it covers                                         |
| ----------------- | ------------------------------------------------------ |
| Orchestrator      | Document indexation, re-indexation, job status         |
| Documents         | Metadata, content, indexation status                   |
| Audit (raw)       | Low-level audit counters & flags (⚠ not the Audit API) |
| Semantic Graph    | Graph nodes, relationships, exploration                |
| Removed endpoints | `/search`, `/conversation` — gone as of 2026-04-13     |
