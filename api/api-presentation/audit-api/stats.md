---
description: >-
  Retrieve audit statistics: daily activity, per-user metrics, and filtered
  aggregates across the audit instance.
---

# Stats

_Authenticated with an OAuth 2.1 Bearer token (MCP) or the `kai_auth` cookie (browsers) — see OAuth 2.1._

***

### POST /audit/stats/get-daily-stats

**`operation_id`:** `audit_stats_get_daily`

Retrieve daily audit statistics for an instance within a date range. Optionally filter by a specific user.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "begin_date": "2026-01-01T00:00:00Z",
  "end_date": "2026-01-31T23:59:59Z",
  "user_id": ""
}
```

| Field         | Type     | Required | Description                                               |
| ------------- | -------- | -------- | --------------------------------------------------------- |
| `instance_id` | string   | yes      | The audit instance ID.                                    |
| `begin_date`  | datetime | yes      | Start of the date range (ISO 8601).                       |
| `end_date`    | datetime | yes      | End of the date range (ISO 8601).                         |
| `user_id`     | string   | no       | Filter by user ID. Empty string or omitted for all users. |

**Response**

```json
{
  "response": { ... }
}
```

Returns daily statistics for the given date range.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/stats/get-daily-stats" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "begin_date": "2026-01-01T00:00:00Z", "end_date": "2026-01-31T23:59:59Z", "user_id": ""}'
```

***

### POST /audit/stats/get-user-stats

**`operation_id`:** `audit_stats_get_user`

Retrieve audit statistics for a specific user within a date range. Non-admin users can only query their own stats.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "begin_date": "2026-01-01T00:00:00Z",
  "end_date": "2026-01-31T23:59:59Z",
  "user_id": "<user-id>"
}
```

| Field         | Type     | Required | Description                                                                |
| ------------- | -------- | -------- | -------------------------------------------------------------------------- |
| `instance_id` | string   | yes      | The audit instance ID.                                                     |
| `begin_date`  | datetime | yes      | Start of the date range (ISO 8601).                                        |
| `end_date`    | datetime | yes      | End of the date range (ISO 8601).                                          |
| `user_id`     | string   | no       | The user ID to query. Empty string for the authenticated user's own stats. |

**Response**

```json
{
  "response": { ... }
}
```

Returns user-level statistics, or `false` if no data is available.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/stats/get-user-stats" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "begin_date": "2026-01-01T00:00:00Z", "end_date": "2026-01-31T23:59:59Z", "user_id": "user_001"}'
```

***

### POST /audit/stats/get-filtered-stats

**`operation_id`:** `audit_stats_get_filtered`

Retrieve aggregated audit statistics filtered by document owner when applicable. Returns a comprehensive summary of the audit's current state.

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
    "total_questions": 150,
    "questions_with_conflicts_to_manage": 23,
    "questions_with_conflicts_analyzed": 18,
    "managed_questions": 12,
    "questions_without_conflicts": 97,
    "missing_subjects_count": 5,
    "total_conflicts": 41,
    "documents_to_update_count": 8,
    "estimated_total_update_time": 3600,
    "questions_not_analyzed_yet": 30
  }
}
```

| Field                                | Description                                          |
| ------------------------------------ | ---------------------------------------------------- |
| `total_questions`                    | Total number of questions in the audit.              |
| `questions_with_conflicts_to_manage` | Questions with unresolved conflicts.                 |
| `questions_with_conflicts_analyzed`  | Questions with conflicts that have been analyzed.    |
| `managed_questions`                  | Questions marked as managed.                         |
| `questions_without_conflicts`        | Questions with no detected conflicts.                |
| `missing_subjects_count`             | Number of missing subjects.                          |
| `total_conflicts`                    | Total number of conflicts across all questions.      |
| `documents_to_update_count`          | Number of documents requiring updates.               |
| `estimated_total_update_time`        | Estimated time (in seconds) to complete all updates. |
| `questions_not_analyzed_yet`         | Questions still awaiting analysis.                   |

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/stats/get-filtered-stats" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123"}'
```
