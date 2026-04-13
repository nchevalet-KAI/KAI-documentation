# Mandatory questions

Manage the mandatory questions associated with an audit instance: list, create, set answers, mark as managed or ignored, generate AI companion recommendations, and force re-analysis.

_Authenticated with an OAuth 2.1 Bearer token (MCP) or the `kai_auth` cookie (browsers) — see OAuth 2.1._

***

### POST /audit/mandatory-question/list

**`operation_id`:** `audit_mandatory_question_list`

List mandatory questions for an audit instance with pagination and optional state filtering.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "offset": 0,
  "limit": 50,
  "state": null
}
```

| Field         | Type    | Required | Description                                                                                     |
| ------------- | ------- | -------- | ----------------------------------------------------------------------------------------------- |
| `instance_id` | string  | yes      | The audit instance ID.                                                                          |
| `offset`      | integer | yes      | Pagination offset (0–100000).                                                                   |
| `limit`       | integer | yes      | Number of results (1–1000).                                                                     |
| `state`       | string  | no       | Filter by question state (e.g. `REFUSED`, `MANAGED`, `IGNORED`). Omit or `null` for all states. |

**Response**

```json
{
  "response": [
    {
      "id": "mq_001",
      "question": "Does the document set cover fire safety procedures?",
      "state": "PENDING",
      "answer": null
    }
  ]
}
```

Returns an array of mandatory question objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/mandatory-question/list" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "offset": 0, "limit": 50}'
```

***

### POST /audit/mandatory-question/create

**`operation_id`:** `audit_mandatory_question_create`

Create a new mandatory question for an audit instance.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "question": "Does the document set cover fire safety procedures?"
}
```

| Field         | Type   | Required | Description                  |
| ------------- | ------ | -------- | ---------------------------- |
| `instance_id` | string | yes      | The audit instance ID.       |
| `question`    | string | yes      | The mandatory question text. |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the question was created successfully, `false` otherwise.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/mandatory-question/create" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "question": "Does the document set cover fire safety procedures?"}'
```

***

### POST /audit/mandatory-question/set-answer

**`operation_id`:** `audit_mandatory_question_set_answer`

Set or update the answer for a mandatory question.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "question_id": "<question-id>",
  "answer": "Yes, covered in section 4.2 of the safety manual."
}
```

| Field         | Type   | Required | Description                |
| ------------- | ------ | -------- | -------------------------- |
| `instance_id` | string | yes      | The audit instance ID.     |
| `question_id` | string | yes      | The mandatory question ID. |
| `answer`      | string | yes      | The answer text.           |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the answer was set successfully, `false` otherwise.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/mandatory-question/set-answer" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "question_id": "mq_001", "answer": "Yes, covered in section 4.2 of the safety manual."}'
```

***

### POST /audit/mandatory-question/set-managed

**`operation_id`:** `audit_mandatory_question_set_managed`

Mark a mandatory question as managed. This triggers document reindexation for all documents referenced by the question's conflicts.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "question_id": "<question-id>"
}
```

| Field         | Type   | Required | Description                |
| ------------- | ------ | -------- | -------------------------- |
| `instance_id` | string | yes      | The audit instance ID.     |
| `question_id` | string | yes      | The mandatory question ID. |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the question was marked as managed, `false` otherwise.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/mandatory-question/set-managed" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "question_id": "mq_001"}'
```

***

### POST /audit/mandatory-question/set-ignored

**`operation_id`:** `audit_mandatory_question_set_ignored`

Mark a mandatory question as ignored by the user.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "question_id": "<question-id>"
}
```

| Field         | Type   | Required | Description                |
| ------------- | ------ | -------- | -------------------------- |
| `instance_id` | string | yes      | The audit instance ID.     |
| `question_id` | string | yes      | The mandatory question ID. |

**Response**

```json
{
  "response": true
}
```

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/mandatory-question/set-ignored" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "question_id": "mq_001"}'
```

***

### POST /audit/mandatory-question/generate-compagnon-answer

**`operation_id`:** `audit_mandatory_question_generate_compagnon_answer`

Generate an AI companion recommendation for a mandatory question based on its conflicts. All conflicts associated with the question must have answers before calling this endpoint. Returns a cached recommendation if one has already been generated.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "question_id": "<question-id>"
}
```

| Field         | Type   | Required | Description                |
| ------------- | ------ | -------- | -------------------------- |
| `instance_id` | string | yes      | The audit instance ID.     |
| `question_id` | string | yes      | The mandatory question ID. |

**Response**

```json
{
  "response": "Based on the conflict analysis, the recommended answer is..."
}
```

Returns the AI-generated recommendation string.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/mandatory-question/generate-compagnon-answer" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "question_id": "mq_001"}'
```

***

### POST /audit/mandatory-question/force-analyze

**`operation_id`:** `audit_mandatory_question_force_analyze`

Force re-analysis of a refused mandatory question. Re-embeds the question and launches a background analysis task. Only works on questions in `REFUSED` state.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "question_id": "<question-id>"
}
```

| Field         | Type   | Required | Description                                             |
| ------------- | ------ | -------- | ------------------------------------------------------- |
| `instance_id` | string | yes      | The audit instance ID.                                  |
| `question_id` | string | yes      | The mandatory question ID (must be in `REFUSED` state). |

**Response**

```json
{
  "response": true
}
```

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/mandatory-question/force-analyze" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "question_id": "mq_001"}'
```
