# Audit (raw primitives)

{% hint style="warning" %}
**Do not confuse with the Audit API.** These endpoints are raw audit primitives exposed by the instance itself — low-level counters and flags, consumed machine-to-machine. The full audit workflow (state machine, duplicates, conflicts, questions, MCP integration) lives on the separate **Audit API** at `api-audit.kai-studio.ai`.
{% endhint %}

_Authenticated with `instance-id` + `api-key` headers — see Instance API keys._

***

### POST /api/audit/conflict-information

List all conflicts with optional search, pagination, document name filtering, and state filtering.

**Request body**

```json
{
  "query": "safety regulation",
  "document_name": "report-2025.pdf",
  "limit": 200,
  "offset": 0,
  "state": "detected",
  "document_ids": ["doc_abc123"]
}
```

| Field           | Type             | Required | Default | Description                                                    |
| --------------- | ---------------- | -------- | ------- | -------------------------------------------------------------- |
| `query`         | string           | no       | `null`  | Free-text search within conflicts.                             |
| `document_name` | string           | no       | `null`  | Filter by document name.                                       |
| `limit`         | integer          | no       | `200`   | Maximum number of conflicts to return.                         |
| `offset`        | integer          | no       | `0`     | Pagination offset.                                             |
| `state`         | string           | no       | `null`  | Filter by conflict state: `detected`, `managed`, or `ignored`. |
| `document_ids`  | array of strings | no       | `null`  | Restrict to conflicts involving these documents.               |

**Response**

```json
{
  "response": [
    {
      "id": "<conflict-id>",
      "state": "detected",
      "subject": "...",
      "document_ids": ["doc_abc123", "doc_def456"]
    }
  ]
}
```

Returns a list of conflict objects.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/conflict-information" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"limit": 200, "offset": 0}'
```

***

### POST /api/audit/conflict-information/set-state

Update a conflict's state. Valid states are `managed`, `ignored`, and `detected`. When the state is set to `managed`, the associated documents are automatically queued for reindexation.

**Request body**

```json
{
  "id": "<conflict-id>",
  "state": "managed"
}
```

| Field   | Type   | Required | Description                                     |
| ------- | ------ | -------- | ----------------------------------------------- |
| `id`    | string | yes      | The conflict ID.                                |
| `state` | string | yes      | New state: `managed`, `ignored`, or `detected`. |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the state was successfully updated.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/conflict-information/set-state" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "conflict_001", "state": "managed"}'
```

***

### POST /api/audit/get-conflict-information

Retrieve a specific conflict by its ID.

**Request body**

```json
{
  "id": "<conflict-id>"
}
```

| Field | Type   | Required | Description      |
| ----- | ------ | -------- | ---------------- |
| `id`  | string | yes      | The conflict ID. |

**Response**

```json
{
  "response": {
    "id": "<conflict-id>",
    "state": "detected",
    "subject": "...",
    "document_ids": ["doc_abc123", "doc_def456"]
  }
}
```

Returns a single conflict object.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/get-conflict-information" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "conflict_001"}'
```

***

### POST /api/audit/get-conflict-information-by-subject

Retrieve all conflicts filtered by subject, with pagination and optional state filtering.

**Request body**

```json
{
  "subject": "safety requirements",
  "limit": 200,
  "offset": 0,
  "state": "detected"
}
```

| Field     | Type    | Required | Default | Description                                                                         |
| --------- | ------- | -------- | ------- | ----------------------------------------------------------------------------------- |
| `subject` | string  | no       | `null`  | Subject to filter by.                                                               |
| `limit`   | integer | no       | `200`   | Maximum number of conflicts to return.                                              |
| `offset`  | integer | no       | `0`     | Pagination offset.                                                                  |
| `state`   | string  | no       | `""`    | Filter by state: `detected`, `managed`, or `ignored`. Empty string means no filter. |

**Response**

```json
{
  "response": [
    {
      "id": "<conflict-id>",
      "state": "detected",
      "subject": "safety requirements",
      "document_ids": ["doc_abc123", "doc_def456"]
    }
  ]
}
```

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/get-conflict-information-by-subject" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"subject": "safety requirements", "limit": 200, "offset": 0}'
```

***

### POST /api/audit/count-conflict-information

Count all conflicts in the instance.

**Request body**

No request body.

**Response**

```json
{
  "response": 27
}
```

Returns the total number of conflicts as an integer.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/count-conflict-information" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>"
```

***

### POST /api/audit/count-conflict-by-subject

Count conflict anomalies grouped by subject. Optionally filter by document IDs and/or state.

**Request body**

```json
{
  "document_ids": ["doc_abc123"],
  "state": "detected"
}
```

| Field          | Type             | Required | Default | Description                                                |
| -------------- | ---------------- | -------- | ------- | ---------------------------------------------------------- |
| `document_ids` | array of strings | no       | `null`  | Restrict the count to conflicts involving these documents. |
| `state`        | string           | no       | `""`    | Filter by state. Empty string means no filter.             |

**Response**

```json
{
  "response": {
    "safety requirements": 5,
    "compliance deadlines": 3
  }
}
```

Returns a dictionary mapping subject names to conflict counts.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/count-conflict-by-subject" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"state": "detected"}'
```

***

### POST /api/audit/count-conflict-by-date

Count conflict anomalies grouped by date. Optionally filter by date range and/or state.

**Request body**

```json
{
  "begin_date": "2025-01-01",
  "end_date": "2025-12-31",
  "state": "detected"
}
```

| Field        | Type   | Required | Default | Description                                   |
| ------------ | ------ | -------- | ------- | --------------------------------------------- |
| `begin_date` | string | no       | `null`  | Start date (inclusive). Format: `YYYY-MM-DD`. |
| `end_date`   | string | no       | `null`  | End date (inclusive). Format: `YYYY-MM-DD`.   |
| `state`      | string | no       | `null`  | Filter by state.                              |

**Response**

```json
{
  "response": {
    "2025-03-15": {
      "detected": 3,
      "managed": 1
    },
    "2025-04-02": {
      "detected": 2
    }
  }
}
```

Returns a nested dictionary: date -> state -> count.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/count-conflict-by-date" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"begin_date": "2025-01-01", "end_date": "2025-12-31"}'
```

***

### POST /api/audit/count-conflicts-by-state

Count conflict anomalies grouped by state. Optionally filter to a single state.

**Request body**

```json
{
  "state": "detected"
}
```

| Field   | Type   | Required | Default | Description                                      |
| ------- | ------ | -------- | ------- | ------------------------------------------------ |
| `state` | string | no       | `null`  | If provided, count only conflicts in this state. |

**Response**

```json
{
  "response": {
    "detected": 15,
    "managed": 8,
    "ignored": 4
  }
}
```

Returns a nested dictionary of state counts.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/count-conflicts-by-state" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{}'
```

***

### POST /api/audit/count-conflict-by-document-ids

Count conflict anomalies for specific document IDs, optionally filtered by state.

**Request body**

```json
{
  "document_ids": ["doc_abc123", "doc_def456"],
  "state": ""
}
```

| Field          | Type             | Required | Default | Description                                    |
| -------------- | ---------------- | -------- | ------- | ---------------------------------------------- |
| `document_ids` | array of strings | no       | `null`  | Document IDs to count conflicts for.           |
| `state`        | string           | no       | `""`    | Filter by state. Empty string means no filter. |

**Response**

```json
{
  "response": {
    "doc_abc123": 4,
    "doc_def456": 1
  }
}
```

Returns a dictionary mapping document IDs to conflict counts.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/count-conflict-by-document-ids" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"document_ids": ["doc_abc123", "doc_def456"]}'
```

***

### POST /api/audit/document-ids-to-manage

Count duplicates and conflicts per document. Useful for identifying which documents need attention. Supports search, pagination, and filtering.

**Request body**

```json
{
  "query": null,
  "document_name": null,
  "limit": 200,
  "offset": 0,
  "state": null,
  "document_ids": null
}
```

| Field           | Type             | Required | Default | Description                     |
| --------------- | ---------------- | -------- | ------- | ------------------------------- |
| `query`         | string           | no       | `null`  | Free-text search.               |
| `document_name` | string           | no       | `null`  | Filter by document name.        |
| `limit`         | integer          | no       | `200`   | Maximum number of entries.      |
| `offset`        | integer          | no       | `0`     | Pagination offset.              |
| `state`         | string           | no       | `null`  | Filter by anomaly state.        |
| `document_ids`  | array of strings | no       | `null`  | Restrict to these document IDs. |

**Response**

```json
{
  "response": {
    "doc_abc123": {
      "conflicts": 3,
      "duplicates": 1
    },
    "doc_def456": {
      "conflicts": 0,
      "duplicates": 2
    }
  }
}
```

Returns a nested dictionary: document ID -> `{conflicts, duplicates}` counts.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/document-ids-to-manage" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"limit": 200, "offset": 0}'
```

***

### POST /api/audit/get-anomalies-for-document

Retrieve all conflicts and duplicates associated with a specific document.

**Request body**

```json
{
  "id": "<document-id>"
}
```

| Field | Type   | Required | Description      |
| ----- | ------ | -------- | ---------------- |
| `id`  | string | no       | The document ID. |

**Response**

```json
{
  "response": {
    "conflicts": [
      {
        "id": "<conflict-id>",
        "state": "detected",
        "subject": "...",
        "document_ids": ["doc_abc123", "doc_def456"]
      }
    ]
  }
}
```

Returns an object containing a `conflicts` array of conflict objects associated with the document.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/get-anomalies-for-document" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "doc_abc123"}'
```

***

### POST /api/audit/document-is-analyzed

Check whether a document has already been audited.

**Request body**

```json
{
  "id": "<document-id>"
}
```

| Field | Type   | Required | Description      |
| ----- | ------ | -------- | ---------------- |
| `id`  | string | no       | The document ID. |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the document has been audited, `false` otherwise.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/document-is-analyzed" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "doc_abc123"}'
```

***

### POST /api/audit/get-conflict-document-pair

Retrieve document ID pairs that have potential conflicts between them. Supports pagination, filtering by document name, state, and ordering.

**Request body**

```json
{
  "limit": 200,
  "offset": 0,
  "document_name": null,
  "state": null,
  "order": "desc"
}
```

| Field           | Type    | Required | Default  | Description                        |
| --------------- | ------- | -------- | -------- | ---------------------------------- |
| `limit`         | integer | no       | `200`    | Maximum number of pairs to return. |
| `offset`        | integer | no       | `0`      | Pagination offset.                 |
| `document_name` | string  | no       | `null`   | Filter by document name.           |
| `state`         | string  | no       | `null`   | Filter by conflict state.          |
| `order`         | string  | no       | `"desc"` | Sort order: `"desc"` or `"asc"`.   |

**Response**

```json
{
  "response": [
    {
      "document_ids": ["doc_abc123", "doc_def456"],
      "conflict_count": 3
    }
  ]
}
```

Returns a list of document pairs with conflict information.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/get-conflict-document-pair" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"limit": 200, "offset": 0, "order": "desc"}'
```

***

### POST /api/audit/get-conflicts-by-document-id-pair

Retrieve all conflicts for a given pair of document IDs. Supports pagination and state filtering.

**Request body**

```json
{
  "document_ids": ["doc_abc123", "doc_def456"],
  "limit": 200,
  "offset": 0,
  "state": null
}
```

| Field          | Type             | Required | Default | Description                            |
| -------------- | ---------------- | -------- | ------- | -------------------------------------- |
| `document_ids` | array of strings | no       | `null`  | The two document IDs forming the pair. |
| `limit`        | integer          | no       | `200`   | Maximum number of conflicts to return. |
| `offset`       | integer          | no       | `0`     | Pagination offset.                     |
| `state`        | string           | no       | `null`  | Filter by conflict state.              |

**Response**

```json
{
  "response": [
    {
      "id": "<conflict-id>",
      "state": "detected",
      "subject": "...",
      "document_ids": ["doc_abc123", "doc_def456"]
    }
  ]
}
```

Returns a list of conflict objects for the specified document pair.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/get-conflicts-by-document-id-pair" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"document_ids": ["doc_abc123", "doc_def456"], "limit": 200, "offset": 0}'
```

***

### POST /api/audit/list-all-document-ids

Get all document IDs that have anomalies (conflicts or duplicates). Supports search, pagination, and filtering.

**Request body**

```json
{
  "query": null,
  "document_name": null,
  "limit": 200,
  "offset": 0,
  "state": null,
  "document_ids": null
}
```

| Field           | Type             | Required | Default | Description                      |
| --------------- | ---------------- | -------- | ------- | -------------------------------- |
| `query`         | string           | no       | `null`  | Free-text search.                |
| `document_name` | string           | no       | `null`  | Filter by document name.         |
| `limit`         | integer          | no       | `200`   | Maximum number of IDs to return. |
| `offset`        | integer          | no       | `0`     | Pagination offset.               |
| `state`         | string           | no       | `null`  | Filter by anomaly state.         |
| `document_ids`  | array of strings | no       | `null`  | Restrict to these document IDs.  |

**Response**

```json
{
  "response": ["doc_abc123", "doc_def456", "doc_ghi789"]
}
```

Returns a list of document IDs with anomalies.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/audit/list-all-document-ids" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"limit": 200, "offset": 0}'
```
