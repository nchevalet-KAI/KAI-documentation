---
description: >-
  Manage audit instances: list, retrieve, create, delete, update workflow steps
  and configuration. This page also covers user membership administration
  (adding/removing users, setting roles).
---

# Instances

_Authenticated with an OAuth 2.1 Bearer token (MCP) or the `kai_auth` cookie (browsers) — see OAuth 2.1._

***

### POST /audit/instance/list-instances-for-user

**`operation_id`:** `audit_instance_list_for_user`

List all audit instances accessible by the authenticated user.

**Request body**

No request body.

**Response**

```json
{
  "response": [
    {
      "id": "inst_abc123",
      "name": "Q1 Compliance Audit",
      "step": "RUNNING_PHASE",
      "configuration": { "need_detect_owner_document_feature": false }
    }
  ]
}
```

Returns an array of audit instance objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/instance/list-instances-for-user" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json"
```

***

### POST /audit/instance/get-instance

**`operation_id`:** `audit_instance_get`

Retrieve detailed information for a specific audit instance, including its current workflow step, API key, and configuration.

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
    "id": "inst_abc123",
    "name": "Q1 Compliance Audit",
    "step": "RUNNING_PHASE",
    "api_key": "ak_...",
    "configuration": {
      "need_detect_owner_document_feature": false
    }
  }
}
```

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/instance/get-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123"}'
```

***

### POST /audit/instance/get-kai-instances

**`operation_id`:** `audit_instance_get_kai_instances`

List all KAI document instances linked to an audit instance. Each audit instance can reference one or more KAI instances that hold the underlying document repositories and vector embeddings.

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
      "id": "link_001",
      "instance_id": "inst_abc123",
      "kai_instance_id": "kai_xyz789",
      "kai_api_key": "ak_...",
      "reason": "Primary document source"
    }
  ]
}
```

Returns an array of KAI instance link objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/instance/get-kai-instances" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123"}'
```

***

### POST /audit/instance/delete-kai-instance

**`operation_id`:** `audit_instance_delete_kai_instance`

Remove a KAI document instance from an audit instance. This unlinks the KAI instance; it does not delete the KAI instance itself.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "kai_instance_id": "<kai-instance-id>"
}
```

| Field             | Type   | Required | Description                    |
| ----------------- | ------ | -------- | ------------------------------ |
| `instance_id`     | string | yes      | The audit instance ID.         |
| `kai_instance_id` | string | yes      | The KAI instance ID to unlink. |

**Response**

```json
{
  "response": {
    "success": true
  }
}
```

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/instance/delete-kai-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "kai_instance_id": "kai_xyz789"}'
```

***

### POST /audit/instance/add-kai-instance

**`operation_id`:** `audit_instance_add_kai_instance`

Link a new KAI document instance to an audit instance.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "kai_instance_id": "<kai-instance-id>",
  "kai_api_key": "<kai-api-key>",
  "reason": "Primary document source"
}
```

| Field             | Type   | Required | Description                    |
| ----------------- | ------ | -------- | ------------------------------ |
| `instance_id`     | string | yes      | The audit instance ID.         |
| `kai_instance_id` | string | yes      | The KAI instance ID to link.   |
| `kai_api_key`     | string | yes      | API key for the KAI instance.  |
| `reason`          | string | yes      | Reason or label for this link. |

**Response**

```json
{
  "response": {
    "success": true
  }
}
```

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/instance/add-kai-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "kai_instance_id": "kai_xyz789", "kai_api_key": "ak_...", "reason": "Primary document source"}'
```

***

### POST /audit/instance/update-instance-step

**`operation_id`:** `audit_instance_update_step`

Update the current workflow step of an audit instance. The audit lifecycle follows this state machine:

`INIT` → `ON_CHECKING_INDEXATION` → `CHECK_INDEXATION_DONE` → `LAUNCH_DUPLICATE_IDENTIFICATION` → `ON_DUPLICATE_IDENTIFICATION` → `DUPLICATE_IDENTIFICATION_DONE` → `RUNNING_PHASE`

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "step": "ON_CHECKING_INDEXATION"
}
```

| Field         | Type   | Required | Description                                                                                                                                                                                         |
| ------------- | ------ | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `instance_id` | string | yes      | The audit instance ID.                                                                                                                                                                              |
| `step`        | string | yes      | Target step. One of: `INIT`, `ON_CHECKING_INDEXATION`, `CHECK_INDEXATION_DONE`, `LAUNCH_DUPLICATE_IDENTIFICATION`, `ON_DUPLICATE_IDENTIFICATION`, `DUPLICATE_IDENTIFICATION_DONE`, `RUNNING_PHASE`. |

**Response**

```json
{
  "response": {
    "success": true
  }
}
```

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/instance/update-instance-step" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "step": "ON_CHECKING_INDEXATION"}'
```

***

### POST /audit/instance/update-configuration

**`operation_id`:** `audit_instance_update_configuration`

Update the configuration settings of an audit instance.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "configuration": {
    "need_detect_owner_document_feature": true
  }
}
```

| Field                                              | Type    | Required | Description                                                                                                      |
| -------------------------------------------------- | ------- | -------- | ---------------------------------------------------------------------------------------------------------------- |
| `instance_id`                                      | string  | yes      | The audit instance ID.                                                                                           |
| `configuration`                                    | object  | yes      | Configuration object.                                                                                            |
| `configuration.need_detect_owner_document_feature` | boolean | no       | Enable document-owner detection. Defaults to `false`. When enabled, non-admin users only see documents they own. |

**Response**

```json
{
  "response": {
    "success": true
  }
}
```

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/instance/update-configuration" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "configuration": {"need_detect_owner_document_feature": true}}'
```

***

### User membership (admin)

The following endpoints manage user membership and roles within audit instances. They require instance admin or global admin privileges (except where noted).

***

### POST /audit/user/get-users-for-instance

**`operation_id`:** `audit_user_get_users`

List all users associated with an audit instance, with pagination. Accessible by instance members and global admins.

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
      "id": "user_001",
      "username": "jdoe",
      "email": "jdoe@example.com"
    }
  ]
}
```

Returns an array of user objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/user/get-users-for-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "offset": 0, "limit": 50}'
```

***

### POST /audit/user/list-user-instances

**`operation_id`:** `audit_user_list_instances`

List all audit instances for a user within an organization. Global admins can query any user; others can only query themselves.

**Request body**

```json
{
  "user_id": "<user-id>",
  "organization_id": "<organization-id>"
}
```

| Field             | Type   | Required | Description           |
| ----------------- | ------ | -------- | --------------------- |
| `user_id`         | string | yes      | The user ID to query. |
| `organization_id` | string | yes      | The organization ID.  |

**Response**

```json
{
  "response": [
    {
      "id": "inst_abc123",
      "name": "Q1 Compliance Audit"
    }
  ]
}
```

Returns an array of audit instance objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/user/list-user-instances" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"user_id": "user_001", "organization_id": "org_abc"}'
```

***

### POST /audit/user/add-user-to-instance

**`operation_id`:** `audit_user_add`

Add a user to an audit instance. Requires instance admin or global admin privileges.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "username": "jdoe",
  "email": "jdoe@example.com"
}
```

| Field         | Type   | Required | Description                  |
| ------------- | ------ | -------- | ---------------------------- |
| `instance_id` | string | yes      | The audit instance ID.       |
| `username`    | string | yes      | Username of the user to add. |
| `email`       | string | yes      | Email of the user to add.    |

**Response**

```json
{
  "response": { ... }
}
```

Returns the result of the add operation.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/user/add-user-to-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "username": "jdoe", "email": "jdoe@example.com"}'
```

***

### POST /audit/user/remove-user-from-instance

**`operation_id`:** `audit_user_remove`

Remove a user from an audit instance. Requires instance admin or global admin privileges.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "user_id": "<user-id>"
}
```

| Field         | Type   | Required | Description            |
| ------------- | ------ | -------- | ---------------------- |
| `instance_id` | string | yes      | The audit instance ID. |
| `user_id`     | string | yes      | The user ID to remove. |

**Response**

```json
{
  "response": { ... }
}
```

Returns the result of the removal operation.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/user/remove-user-from-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "user_id": "user_001"}'
```

***

### POST /audit/user/set-user-admin-for-instance

**`operation_id`:** `audit_user_set_admin`

Promote a user to admin role for an audit instance. Requires instance admin or global admin privileges.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "user_id": "<user-id>"
}
```

| Field         | Type   | Required | Description             |
| ------------- | ------ | -------- | ----------------------- |
| `instance_id` | string | yes      | The audit instance ID.  |
| `user_id`     | string | yes      | The user ID to promote. |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the promotion succeeded, `false` otherwise.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/user/set-user-admin-for-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "user_id": "user_001"}'
```

***

### POST /audit/user/set-user-normal-for-instance

**`operation_id`:** `audit_user_set_normal`

Demote a user to regular (non-admin) role for an audit instance. Requires instance admin or global admin privileges.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "user_id": "<user-id>"
}
```

| Field         | Type   | Required | Description            |
| ------------- | ------ | -------- | ---------------------- |
| `instance_id` | string | yes      | The audit instance ID. |
| `user_id`     | string | yes      | The user ID to demote. |

**Response**

```json
{
  "response": true
}
```

Returns `true` if the demotion succeeded, `false` otherwise.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/user/set-user-normal-for-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "user_id": "user_001"}'
```

***

### POST /audit/user/user-is-admin-for-instance

**`operation_id`:** `audit_user_is_admin`

Check whether the authenticated user has admin privileges for an audit instance.

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
  "response": true
}
```

Returns `true` if the current user is an admin for this instance, `false` otherwise.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/user/user-is-admin-for-instance" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123"}'
```
