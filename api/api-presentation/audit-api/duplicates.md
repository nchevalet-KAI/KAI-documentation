# Duplicates

List and manage duplicate document clusters detected during the audit lifecycle. Duplicate identification is part of the audit state machine — it runs as a background task during the `ON_DUPLICATE_IDENTIFICATION` step, after indexation has been verified.

_Authenticated with an OAuth 2.1 Bearer token (MCP) or the `kai_auth` cookie (browsers) — see OAuth 2.1._

***

### POST /audit/duplicate/list-duplicates-for-instance

**`operation_id`:** `audit_duplicate_list`

List duplicate document clusters for an audit instance with pagination.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "offset": 0,
  "limit": 50
}
```

| Field         | Type    | Required | Description                   |
| ------------- | ------- | -------- | ----------------------------- |
| `instance_id` | string  | yes      | The audit instance ID.        |
| `offset`      | integer | yes      | Pagination offset (0–100000). |
| `limit`       | integer | yes      | Number of results (1–1000).   |

**Response**

```json
{
  "response": [
    {
      "id": "cluster_001",
      "documents": ["doc_001", "doc_002"],
      "managed": false
    }
  ]
}
```

Returns an array of duplicate cluster objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/duplicate/list-duplicates-for-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "offset": 0, "limit": 50}'
```

***

### POST /audit/duplicate/set-managed

**`operation_id`:** `audit_duplicate_set_managed`

Mark a duplicate cluster as managed and trigger verification via KAI instance reindex.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "id": "<cluster-id>"
}
```

| Field         | Type   | Required | Description               |
| ------------- | ------ | -------- | ------------------------- |
| `instance_id` | string | yes      | The audit instance ID.    |
| `id`          | string | yes      | The duplicate cluster ID. |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the cluster was successfully marked as managed, `false` otherwise.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/duplicate/set-managed" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "id": "cluster_001"}'
```
