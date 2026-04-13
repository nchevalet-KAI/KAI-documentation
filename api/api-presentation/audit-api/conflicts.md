# Conflicts

List and manage conflicts detected during the audit. A conflict represents a contradiction or inconsistency found across documents in the audit instance. When `need_detect_owner_document_feature` is enabled, non-admin users only see conflicts on documents they own.

_Authenticated with an OAuth 2.1 Bearer token (MCP) or the `kai_auth` cookie (browsers) — see OAuth 2.1._

***

### POST /audit/conflict/list-conflicts-for-instance

**`operation_id`:** `audit_conflict_list`

List all conflicts for an audit instance with pagination and optional owner filtering.

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
      "id": "conflict_001",
      "question": "What is the maximum load capacity?",
      "state": "PENDING"
    }
  ]
}
```

Returns an array of conflict objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/conflict/list-conflicts-for-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "offset": 0, "limit": 50}'
```

***

### POST /audit/conflict/get

**`operation_id`:** `audit_conflict_get`

Retrieve detailed information for a specific conflict, including the conflicting excerpts and associated documents.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "conflict_id": "<conflict-id>"
}
```

| Field         | Type   | Required | Description            |
| ------------- | ------ | -------- | ---------------------- |
| `instance_id` | string | yes      | The audit instance ID. |
| `conflict_id` | string | yes      | The conflict ID.       |

**Response**

```json
{
  "response": { ... }
}
```

Returns the full conflict detail object.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/conflict/get" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "conflict_id": "conflict_001"}'
```

***

### POST /audit/conflict/set-answer

**`operation_id`:** `audit_conflict_set_answer`

Set or update the audit answer for a specific conflict.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "conflict_id": "<conflict-id>",
  "answer": "The 500kg figure in doc_002 is correct; doc_001 is outdated."
}
```

| Field         | Type   | Required | Description                 |
| ------------- | ------ | -------- | --------------------------- |
| `instance_id` | string | yes      | The audit instance ID.      |
| `conflict_id` | string | yes      | The conflict ID.            |
| `answer`      | string | yes      | The resolution answer text. |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the answer was recorded, `false` otherwise.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/conflict/set-answer" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "conflict_id": "conflict_001", "answer": "The 500kg figure in doc_002 is correct; doc_001 is outdated."}'
```

***

### POST /audit/conflict/get-top-collaborators

**`operation_id`:** `audit_conflict_get_top_collaborators`

Get the top collaborators sharing conflicts with the current user. Returns up to 3 collaborators. Returns an empty list for admin users.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>"
}
```

| Field         | Type   | Required | Description            |
| ------------- | ------ | -------- | ---------------------- |
| `instance_id` | string | yes      | The audit instance ID. |

**Response**

```json
{
  "response": [
    {
      "user_id": "user_002",
      "username": "asmith",
      "shared_conflict_count": 12
    }
  ]
}
```

Returns an array of collaborator objects (up to 3).

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/conflict/get-top-collaborators" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123"}'
```
