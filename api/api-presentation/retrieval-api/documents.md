---
description: >-
  Fetch document metadata and content from instances the authenticated user can
  access.
---

# Documents

_Authenticated with an OAuth 2.1 Bearer token or the `kai_auth` cookie — see OAuth 2.1._

***

### POST /retrieval/documents/list

Returns a paginated list of all documents in a knowledge base. Use after semantic search to explore more content in the same instance.

**Request body**

```json
{
  "instance_id": "inst_abc123",
  "offset": 0,
  "limit": 20
}
```

| Field         | Type  | Required | Constraints | Description                                                                  |
| ------------- | ----- | -------- | ----------- | ---------------------------------------------------------------------------- |
| `instance_id` | `str` | Yes      | —           | ID of the instance to list documents from (from `list-available-instances`). |
| `offset`      | `int` | Yes      | 0 -- 100000 | Number of documents to skip.                                                 |
| `limit`       | `int` | Yes      | 1 -- 1000   | Maximum number of documents to return.                                       |

**Response**

```json
{
  "response": [
    { "..." : "document objects" }
  ]
}
```

The response contains a list of document objects from the specified instance.

**Example**

```bash
curl -X POST "https://api-retrieval.kai-studio.ai/retrieval/documents/list" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "instance_id": "inst_abc123",
    "offset": 0,
    "limit": 20
  }'
```

***

### POST /retrieval/documents/get-document

Get the full content of a specific document. Use the document ID from search results or from the `list` endpoint.

**Request body**

```json
{
  "instance_id": "inst_abc123",
  "document_id": "doc_def456"
}
```

| Field         | Type  | Required | Description                                 |
| ------------- | ----- | -------- | ------------------------------------------- |
| `instance_id` | `str` | Yes      | ID of the instance containing the document. |
| `document_id` | `str` | Yes      | ID of the document to retrieve.             |

**Response**

```json
{
  "response": { "..." : "full document object" }
}
```

The response contains the full document object, including its content.

**Example**

```bash
curl -X POST "https://api-retrieval.kai-studio.ai/retrieval/documents/get-document" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "instance_id": "inst_abc123",
    "document_id": "doc_def456"
  }'
```

***

### POST /retrieval/documents/list-by-ids

Get the full content of multiple documents at once. Use with document IDs from search results to batch-fetch documents in a single call.

**Request body**

```json
{
  "instance_id": "inst_abc123",
  "document_ids": ["doc_def456", "doc_ghi789"]
}
```

| Field          | Type        | Required | Description                                  |
| -------------- | ----------- | -------- | -------------------------------------------- |
| `instance_id`  | `str`       | Yes      | ID of the instance containing the documents. |
| `document_ids` | `List[str]` | Yes      | List of document IDs to retrieve.            |

**Response**

```json
{
  "response": [
    { "..." : "full document object" },
    { "..." : "full document object" }
  ]
}
```

The response contains a list of full document objects matching the requested IDs.

**Example**

```bash
curl -X POST "https://api-retrieval.kai-studio.ai/retrieval/documents/list-by-ids" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "instance_id": "inst_abc123",
    "document_ids": ["doc_def456", "doc_ghi789"]
  }'
```
