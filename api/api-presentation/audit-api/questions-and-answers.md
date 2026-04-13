# Questions & answers

The full audit view surfaces question-level analysis across the audit instance. These endpoints check whether the full audit view is available, retrieve detailed conflict information for a question, and record expert answers.

_Authenticated with an OAuth 2.1 Bearer token (MCP) or the `kai_auth` cookie (browsers) — see OAuth 2.1._

***

### POST /audit/full-audit/have-to-show

**`operation_id`:** `audit_full_audit_have_to_show`

Check whether the full audit view should be displayed for an instance. Returns `true` when the audit has progressed far enough to surface question-level results.

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
  "response": {
    "show": true
  }
}
```

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/full-audit/have-to-show" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123"}'
```

***

### POST /audit/full-audit/detail

**`operation_id`:** `audit_full_audit_get_detail`

Retrieve detailed information for a specific full audit conflict, including the question, conflicting excerpts, and any existing answers.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "conflict_id": "<conflict-id>"
}
```

| Field         | Type   | Required | Description                              |
| ------------- | ------ | -------- | ---------------------------------------- |
| `instance_id` | string | yes      | The audit instance ID.                   |
| `conflict_id` | string | yes      | The conflict ID to retrieve details for. |

**Response**

```json
{
  "response": { ... }
}
```

Returns the full audit detail object for the conflict.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/full-audit/detail" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "conflict_id": "conflict_001"}'
```

***

### POST /audit/full-audit/set-expert-answer

**`operation_id`:** `audit_full_audit_set_expert_answer`

Set an expert answer for a full audit conflict. After the answer is recorded, the system generates companion recommendations based on the expert input.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "conflict_id": "<conflict-id>",
  "answer": "The correct interpretation is..."
}
```

| Field         | Type   | Required | Description             |
| ------------- | ------ | -------- | ----------------------- |
| `instance_id` | string | yes      | The audit instance ID.  |
| `conflict_id` | string | yes      | The conflict ID.        |
| `answer`      | string | yes      | The expert answer text. |

**Response**

```json
{
  "response": {
    "updated": true
  }
}
```

Returns `true` if the expert answer was recorded, `false` otherwise.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/full-audit/set-expert-answer" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "conflict_id": "conflict_001", "answer": "The correct interpretation is..."}'
```
