---
description: >-
  A compact reference of every MCP tool KAI exposes, with links to the full
  endpoint documentation.
---

# MCP tool catalog

### Retrieval MCP (stable)

Server: `https://api-retrieval.kai-studio.ai/mcp`

| Tool (`operation_id`)                          | Endpoint page  | Description                                          |
| ---------------------------------------------- | -------------- | ---------------------------------------------------- |
| `retrieval_instances_list_available_instances` | Instances      | List accessible instances with composed instructions |
| `retrieval_documents_list`                     | Documents      | Paginated list of documents in an instance           |
| `retrieval_documents_get_document`             | Documents      | Fetch the full content of one document               |
| `retrieval_documents_list_by_ids`              | Documents      | Fetch multiple documents by ID in a single call      |
| `retrieval_semantic_nodes_search`              | Semantic nodes | Semantic search across a knowledge base              |

### Audit MCP (Stable)

Server: `https://api-audit.kai-studio.ai/mcp`

The Audit MCP exposes a **curated 19-tool expert surface** — a subset of the 40 REST endpoints. Admin operations (instance create/delete, user management, stats, duplicates, owner assignment) and question-level write operations (`set-answer`, `set-managed`, `set-ignored`, `generate-compagnon-answer`) remain REST-only and are served by `audit-ui`. MCP is built around the **conflict-first workflow**: start at the dashboard, iterate on open conflicts, confirm modifications, close.

#### Workflow entry

| Tool (`operation_id`) | Endpoint page      | Description                                                                                                                 |
| --------------------- | ------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| `audit_dashboard_get` | Audit API overview | Summary of all audit instances with unresolved-conflict / pending-question / missing-subject counts. **Always start here.** |

#### Conflict-first workflow (primary)

| Tool (`operation_id`)        | Endpoint page | Description                                                                                                                             |
| ---------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `audit_conflict_list`        | Conflicts     | List conflicts for an instance (default `state_in=['OPEN']`)                                                                            |
| `audit_conflict_get`         | Conflicts     | Retrieve conflicting excerpts + associated documents                                                                                    |
| `audit_conflict_set_answer`  | Conflicts     | Record expert answer; returns per-document modification recommendations **inline** — render as markdown table with `document_url` links |
| `audit_conflict_set_managed` | Conflicts     | Close the conflict (MANAGED) — call **only after** expert confirms all modifications were applied                                       |

#### Document helpers

| Tool (`operation_id`)                | Endpoint page          | Description                                                                                                            |
| ------------------------------------ | ---------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `audit_document_get_by_ids`          | Documents & indexation | Fetch document metadata (name, URL) for a list of IDs — use after `audit_conflict_get` to resolve source document URLs |
| `audit_document_get_recommendations` | Documents & indexation | Aggregate all pending AI-generated edits on a single document across every resolved conflict                           |

#### Mandatory questions (admin surface)

| Tool (`operation_id`)                    | Endpoint page       | Description                                                          |
| ---------------------------------------- | ------------------- | -------------------------------------------------------------------- |
| `audit_mandatory_question_list`          | Mandatory questions | List mandatory questions with optional state filter (e.g. `REFUSED`) |
| `audit_mandatory_question_create`        | Mandatory questions | Create a new mandatory question for an instance                      |
| `audit_mandatory_question_force_analyze` | Mandatory questions | Force re-analysis of a `REFUSED` question                            |

#### Missing subjects

| Tool (`operation_id`)                               | Endpoint page    | Description                                      |
| --------------------------------------------------- | ---------------- | ------------------------------------------------ |
| `audit_missing_subject_list`                        | Missing subjects | List missing subjects for an instance            |
| `audit_missing_subject_find`                        | Missing subjects | Retrieve detail for a missing subject            |
| `audit_missing_subject_list_questions`              | Missing subjects | List questions associated with a missing subject |
| `audit_missing_subject_set_state`                   | Missing subjects | Update state of a missing subject                |
| `audit_missing_subject_generate_compagnon_document` | Missing subjects | Generate AI companion document proposition       |

#### Full-audit (broad review — out of the conflict-first flow)

Use **only** when the expert explicitly asks for a broad per-instance review across the entire corpus — not for day-to-day conflict resolution.

| Tool (`operation_id`)                | Endpoint page       | Description                                                     |
| ------------------------------------ | ------------------- | --------------------------------------------------------------- |
| `audit_full_audit_list`              | Questions & answers | List full-audit conflicts (excludes `DISAPPEARED`)              |
| `audit_full_audit_get_detail`        | Questions & answers | Detail for a full-audit conflict, enriched with live KAI data   |
| `audit_full_audit_set_state`         | Questions & answers | Update state of a full-audit conflict (`MANAGED`, `IGNORED`, …) |
| `audit_full_audit_set_expert_answer` | Questions & answers | Record expert answer — auto-triggers companion recommendations  |

#### Not exposed on MCP (REST-only)

These operations exist as REST endpoints for `audit-ui` but are intentionally **excluded from the MCP surface**: `audit_instance_*` (list/get/update), `audit_user_*` (membership + role admin), `audit_stats_*` (dashboard stats), `audit_duplicate_*` (duplicate clusters), `audit_document_list` / `audit_document_set_owner` / `audit_document_count` / `audit_document_list_with_state`, `audit_conflict_get_top_collaborators`, `audit_full_audit_have_to_show`, `audit_mandatory_question_set_answer` / `set_managed` / `set_ignored` / `generate_compagnon_answer`.
