---
description: >-
  The Orchestrator endpoints drive document indexation: starting jobs, tracking
  their status, and managing re-indexation.
---

# Orchestrator

_Authenticated with `instance-id` + `api-key` headers — see Instance API keys._

***

### POST /api/orchestrator/differential-indexation

Relaunch partial indexation. All documents that have been created, updated, or deleted in the knowledge base since the last indexation will be reindexed or removed from the KAI index. This process can take a variable amount of time depending on the size of the knowledge base and the complexity of the documents involved.

**Request body**

No request body.

**Response**

```json
{
  "response": true
}
```

Returns `true` if the indexation job was successfully queued.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/orchestrator/differential-indexation" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>"
```

***

### POST /api/orchestrator/reindex-document

Reindex a single document. If the document has been deleted from the knowledge base, it will be removed from the index. If the document has been updated, it will be reindexed with the new content.

**Request body**

```json
{
  "id": "<document-id>"
}
```

| Field | Type   | Required | Description                 |
| ----- | ------ | -------- | --------------------------- |
| `id`  | string | yes      | The document ID to reindex. |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the reindex job was successfully queued.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/orchestrator/reindex-document" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "doc_abc123"}'
```

***

### POST /api/orchestrator/retry-documents-parsing-error

Launch a task to retry indexation for all documents currently in a parsing-error state. Useful after fixing upstream issues (e.g. corrupted files replaced, parser updated).

**Request body**

No request body.

**Response**

```json
{
  "response": true
}
```

Returns `true` if the retry task was successfully launched.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/orchestrator/retry-documents-parsing-error" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>"
```

***

### POST /api/orchestrator/count-back-tasks

Count all registered background tasks. Returns the number of in-progress tasks and tasks waiting to be launched, grouped by agent name.

**Request body**

No request body.

**Response**

```json
{
  "response": {
    "<agent_name>": 3,
    "<agent_name>": 1
  }
}
```

Each key is an agent (task type) name; the value is the count of active or pending tasks for that agent.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/orchestrator/count-back-tasks" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>"
```

***

### POST /api/orchestrator/count-tasks-for-doc

Count registered background tasks for a specific document. Returns the number of in-progress and pending tasks for that document, grouped by agent name.

**Request body**

```json
{
  "id": "<document-id>"
}
```

| Field | Type   | Required | Description                         |
| ----- | ------ | -------- | ----------------------------------- |
| `id`  | string | yes      | The document ID to query tasks for. |

**Response**

```json
{
  "response": {
    "<agent_name>": 2,
    "<agent_name>": 0
  }
}
```

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/orchestrator/count-tasks-for-doc" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "doc_abc123"}'
```

***

### POST /api/orchestrator/check-kb-credentials

Check the validity of knowledge-base credentials. If all credentials are valid, the indexation pipeline is reactivated automatically.

**Request body**

No request body.

**Response**

```json
{
  "response": true
}
```

Returns `true` if all KB credentials are valid and the pipeline has been reactivated. Returns `false` if one or more credentials are invalid.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/orchestrator/check-kb-credentials" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>"
```
