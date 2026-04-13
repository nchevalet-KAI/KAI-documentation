# Missing subjects

List and manage missing subjects identified during the audit. A missing subject represents a topic or area that should be covered by the document set but is not adequately addressed.

_Authenticated with an OAuth 2.1 Bearer token (MCP) or the `kai_auth` cookie (browsers) — see OAuth 2.1._

***

### POST /audit/missing-subject/list

**`operation_id`:** `audit_missing_subject_list`

List missing subjects for an audit instance with pagination.

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
      "id": "ms_001",
      "subject": "Emergency evacuation procedures",
      "state": "PENDING"
    }
  ]
}
```

Returns an array of missing subject objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/missing-subject/list" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "offset": 0, "limit": 50}'
```

***

### POST /audit/missing-subject/find

**`operation_id`:** `audit_missing_subject_find`

Retrieve detailed information for a specific missing subject.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "subject_id": "<subject-id>"
}
```

| Field         | Type   | Required | Description             |
| ------------- | ------ | -------- | ----------------------- |
| `instance_id` | string | yes      | The audit instance ID.  |
| `subject_id`  | string | yes      | The missing subject ID. |

**Response**

```json
{
  "response": { ... }
}
```

Returns the missing subject detail object, or `null` if not found.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/missing-subject/find" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "subject_id": "ms_001"}'
```

***

### POST /audit/missing-subject/questions

**`operation_id`:** `audit_missing_subject_list_questions`

List all questions associated with a specific missing subject. These questions help determine whether the subject is truly missing or partially covered.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "subject_id": "<subject-id>"
}
```

| Field         | Type   | Required | Description             |
| ------------- | ------ | -------- | ----------------------- |
| `instance_id` | string | yes      | The audit instance ID.  |
| `subject_id`  | string | yes      | The missing subject ID. |

**Response**

```json
{
  "response": [
    {
      "id": "msq_001",
      "question": "Is there a section on emergency exits?",
      "answer": null
    }
  ]
}
```

Returns an array of missing subject question objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/missing-subject/questions" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "subject_id": "ms_001"}'
```

***

### POST /audit/missing-subject/set-state

**`operation_id`:** `audit_missing_subject_set_state`

Update the state of a missing subject.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "subject_id": "<subject-id>",
  "state": "MANAGED"
}
```

| Field         | Type   | Required | Description             |
| ------------- | ------ | -------- | ----------------------- |
| `instance_id` | string | yes      | The audit instance ID.  |
| `subject_id`  | string | yes      | The missing subject ID. |
| `state`       | string | yes      | The new state value.    |

**Response**

```json
{
  "response": { ... }
}
```

Returns the result of the state update.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/missing-subject/set-state" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "subject_id": "ms_001", "state": "MANAGED"}'
```

***

### POST /audit/missing-subject/generate-compagnon-document

**`operation_id`:** `audit_missing_subject_generate_compagnon_document`

Generate an AI companion document proposition for a missing subject. All questions associated with the subject must have answers before calling this endpoint. Returns a cached proposition if one has already been generated.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "subject_id": "<subject-id>"
}
```

| Field         | Type   | Required | Description             |
| ------------- | ------ | -------- | ----------------------- |
| `instance_id` | string | yes      | The audit instance ID.  |
| `subject_id`  | string | yes      | The missing subject ID. |

**Response**

```json
{
  "response": "Proposed document outline for emergency evacuation procedures:\n1. Scope and applicability\n2. Evacuation routes..."
}
```

Returns the AI-generated document proposition string.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/missing-subject/generate-compagnon-document" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "subject_id": "ms_001"}'
```
