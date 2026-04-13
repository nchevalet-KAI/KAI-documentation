---
description: >-
  List the KAI instances the authenticated user can access, with the
  instructions that apply to them.
---

# Instances

_Authenticated with an OAuth 2.1 Bearer token or the `kai_auth` cookie — see OAuth 2.1._

### POST /retrieval/instances/list-available-instances

Returns all internal knowledge bases the user can access. Each knowledge base includes a name, description, and composed instructions explaining what topics and documents it contains. The instructions blend organisation defaults, instance configuration, and any group-level overrides that apply to the authenticated user.

Call this endpoint first to discover where to search, then use `semantic-nodes/search` on the chosen instance.

**Request body**

No request body. The user is identified by the access token.

**Response**

```json
{
  "response": [
    {
      "id": "inst_abc123",
      "name": "Safety Regulations",
      "description": "All safety and compliance documents for the EU market.",
      "instructions": "This knowledge base contains safety regulations, compliance checklists, and audit reports. Focus on specific regulation numbers when searching.",
      "organization_id": "org_xyz789"
    }
  ]
}
```

**Field reference**

| Field             | Type          | Description                                                                            |
| ----------------- | ------------- | -------------------------------------------------------------------------------------- |
| `id`              | `str`         | Unique identifier of the KAI instance.                                                 |
| `name`            | `str`         | Display name of the instance.                                                          |
| `description`     | `str \| null` | Optional human-readable description of the instance's content.                         |
| `instructions`    | `str \| null` | Composed instructions for the LLM, describing the instance's topics and how to use it. |
| `organization_id` | `str \| null` | Identifier of the organisation that owns the instance.                                 |

**Example**

```bash
curl -X POST "https://api-retrieval.kai-studio.ai/retrieval/instances/list-available-instances" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json"
```
