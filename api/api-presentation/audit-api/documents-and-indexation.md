# Documents & indexation

List and manage documents within an audit instance. When the `need_detect_owner_document_feature` configuration is enabled, non-admin users only see documents they own.

_Authenticated with an OAuth 2.1 Bearer token (MCP) or the `kai_auth` cookie (browsers) — see OAuth 2.1._

***

### POST /audit/document/list

**`operation_id`:** `audit_document_list`

List documents for an audit instance with pagination. When the instance has `need_detect_owner_document_feature` enabled, non-admin users only see documents assigned to them.

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
      "id": "doc_001",
      "name": "policy_v3.pdf",
      "owner_user_id": "user_001"
    }
  ]
}
```

Returns an array of document objects.

**Example**

```bash
curl -X POST "https://api-audit.kai-studio.ai/audit/document/list" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "offset": 0, "limit": 50}'
```

***

### POST /audit/document/set-owner

**`operation_id`:** `audit_document_set_owner`

Assign or unassign an owner to a document within an audit instance. Admin only. Cannot assign an admin user as document owner. Pass `null` for `owner_user_id` to unassign the current owner.

**Request body**

```json
{
  "instance_id": "<audit-instance-id>",
  "document_id": "<document-id>",
  "owner_user_id": "<user-id>"
}
```

| Field           | Type   | Required | Description                                        |
| --------------- | ------ | -------- | -------------------------------------------------- |
| `instance_id`   | string | yes      | The audit instance ID.                             |
| `document_id`   | string | yes      | The document ID.                                   |
| `owner_user_id` | string | no       | User ID to assign as owner, or `null` to unassign. |

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
curl -X POST "https://api-audit.kai-studio.ai/audit/document/set-owner" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{"instance_id": "inst_abc123", "document_id": "doc_001", "owner_user_id": "user_002"}'
```
