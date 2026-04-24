# Audit API

The **Audit API** drives KAI's document-audit workflow: verifying indexation, identifying duplicates, answering mandatory questions, and surfacing conflicts and missing subjects.

### When to use

Two modes of consumption:

* **Browser (`audit-ui`)** — the production path. End-users log in to `https://audit.kai-studio.ai`, and the UI talks to this API via the `kai_auth` cookie. For day-to-day audit work, you probably do not need this API directly; the UI covers it.
* **MCP 🧪 BETA** — drive an audit from a host LLM (Claude Desktop, Cursor, Le Chat). Useful for automating exploration of an audit's state, batch processing, or integrating audit into an agent.

{% hint style="warning" %}
**BETA notice.** The 40 REST endpoints below are the full Audit API surface. MCP exposes a **curated 19-tool subset** focused on the conflict-first expert workflow — admin, stats, duplicates, user membership, and question-level writes are REST-only. HTTP contracts (paths, request/response shapes) are stable; **MCP tool schemas may still evolve**. Not recommended for production-critical workloads. See MCP usage for the curated MCP surface and current limits, and the MCP tool catalog for the exact list.
{% endhint %}

### Base URL & conventions

* **Base URL:** `https://api-audit.kai-studio.ai`
* **Auth:** Bearer JWT (MCP) or `kai_auth` cookie (browsers). See OAuth 2.1.
* **Methods:** all `POST`, JSON request body.
* **Response shape:** every successful response is wrapped as `{"response": <payload>}`.
* **`operation_id` convention:** `audit_<domain>_<action>` (e.g. `audit_instance_get`, `audit_duplicate_set_managed`). Used as the MCP tool name.
* **Errors:** standard HTTP status codes, body `{"detail": "<message>"}`.

### Endpoint categories

| Page                   | Scope                                                                |
| ---------------------- | -------------------------------------------------------------------- |
| Instances              | list, get, create, delete, step transitions, user membership (admin) |
| Documents & indexation | list documents, assign owners                                        |
| Duplicates             | list duplicate clusters, mark as managed                             |
| Mandatory questions    | list, create, set answers, ignore, AI companion, force re-analysis   |
| Questions & answers    | full audit view, conflict detail, expert answers                     |
| Conflicts              | list, get detail, set answer, top collaborators                      |
| Missing subjects       | list, find, questions, set state, AI companion document              |
| Stats                  | daily stats, user stats, filtered aggregates                         |
| MCP usage (BETA)       | connect Claude Desktop / Cursor / Le Chat                            |
