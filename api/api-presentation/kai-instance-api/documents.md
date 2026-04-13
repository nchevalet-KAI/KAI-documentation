---
description: >-
  The Documents endpoints expose metadata and indexation status for files in the
  instance.
---

# Documents

_Authenticated with `instance-id` + `api-key` headers — see Instance API keys._

***

### POST /api/document/list-docs

List documents from the index. Results may differ from the knowledge base if a differential indexation has not been launched since the last changes.

**Request body**

```json
{
  "offset": 0,
  "limit": 20,
  "state": "INDEXED"
}
```

| Field    | Type    | Required | Default | Description                                        |
| -------- | ------- | -------- | ------- | -------------------------------------------------- |
| `offset` | integer | no       | `0`     | Pagination offset.                                 |
| `limit`  | integer | no       | `20`    | Maximum number of documents to return.             |
| `state`  | string  | no       | `null`  | Filter by document state (see valid states below). |

Valid states: `INITIAL_SAVED`, `UPDATED`, `ON_CONTENT_EXTRACT`, `CONTENT_EXTRACTED`, `PARSING_ERROR`, `ON_INDEXATION`, `INDEXED`.

**Response**

```json
{
  "response": [
    {
      "id": "<document-id>",
      "name": "report-2025.pdf",
      "extraproperties": { }
    }
  ]
}
```

Each document object contains `id`, `name`, and `extraproperties` (a dictionary of metadata set during ingestion).

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/document/list-docs" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"offset": 0, "limit": 20}'
```

***

### POST /api/document/doc

Retrieve detailed information about a single document by its ID.

**Request body**

```json
{
  "id": "<document-id>"
}
```

| Field | Type   | Required | Description      |
| ----- | ------ | -------- | ---------------- |
| `id`  | string | no       | The document ID. |

**Response**

```json
{
  "response": {
    "id": "<document-id>",
    "name": "report-2025.pdf",
    "url": "https://storage.example.com/...",
    "resume": "This document covers...",
    "extraproperties": { }
  }
}
```

| Field             | Type   | Description                             |
| ----------------- | ------ | --------------------------------------- |
| `id`              | string | Unique document identifier.             |
| `name`            | string | File name.                              |
| `url`             | string | Storage URL of the original file.       |
| `resume`          | string | Auto-generated summary of the document. |
| `extraproperties` | object | Metadata dictionary.                    |

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/document/doc" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "doc_abc123"}'
```

***

### POST /api/document/download

Download the original file from storage. Returns a binary stream response.

**Request body**

```json
{
  "id": "<document-id>"
}
```

| Field | Type   | Required | Description                  |
| ----- | ------ | -------- | ---------------------------- |
| `id`  | string | no       | The document ID to download. |

**Response**

Binary stream (`application/octet-stream`). Save the response body to a file.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/document/download" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "doc_abc123"}' \
  -o downloaded-file.pdf
```

***

### POST /api/document/docs-by-ids

Retrieve document information for a list of IDs. Supports pagination.

**Request body**

```json
{
  "ids": ["doc_abc123", "doc_def456"],
  "offset": 0,
  "limit": 20
}
```

| Field    | Type             | Required | Default | Description                            |
| -------- | ---------------- | -------- | ------- | -------------------------------------- |
| `ids`    | array of strings | no       | `[]`    | List of document IDs to retrieve.      |
| `offset` | integer          | no       | `0`     | Pagination offset.                     |
| `limit`  | integer          | no       | `20`    | Maximum number of documents to return. |

**Response**

```json
{
  "response": [
    {
      "id": "<document-id>",
      "name": "report-2025.pdf",
      "url": "https://storage.example.com/...",
      "extraproperties": { }
    }
  ]
}
```

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/document/docs-by-ids" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"ids": ["doc_abc123", "doc_def456"], "offset": 0, "limit": 20}'
```

***

### POST /api/document/count-documents

Count documents in the index, optionally filtered by state and/or a list of document IDs.

**Request body**

```json
{
  "state": "INDEXED",
  "document_ids": ["doc_abc123"]
}
```

| Field          | Type             | Required | Default | Description                                                                                                                                                 |
| -------------- | ---------------- | -------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `state`        | string           | no       | `null`  | Filter by document state. Valid values: `INITIAL_SAVED`, `UPDATED`, `ON_CONTENT_EXTRACT`, `CONTENT_EXTRACTED`, `PARSING_ERROR`, `ON_INDEXATION`, `INDEXED`. |
| `document_ids` | array of strings | no       | `null`  | Restrict the count to these document IDs.                                                                                                                   |

**Response**

```json
{
  "response": 42
}
```

Returns the integer count of matching documents.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/document/count-documents" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"state": "INDEXED"}'
```

***

### POST /api/document/count-documents-per-date

Get document statistics between two dates.

**Request body**

```json
{
  "begin_date": "2025-01-01",
  "end_date": "2025-12-31"
}
```

| Field        | Type   | Required | Default | Description                                   |
| ------------ | ------ | -------- | ------- | --------------------------------------------- |
| `begin_date` | string | no       | `null`  | Start date (inclusive). Format: `YYYY-MM-DD`. |
| `end_date`   | string | no       | `null`  | End date (inclusive). Format: `YYYY-MM-DD`.   |

**Response**

```json
{
  "response": {
    "2025-01-15": 5,
    "2025-02-03": 12
  }
}
```

Returns a dictionary mapping dates to document counts.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/document/count-documents-per-date" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"begin_date": "2025-01-01", "end_date": "2025-12-31"}'
```

***

### POST /api/document/kb-meta-fields

Retrieve all metadata fields available from the knowledge base for a document. These are the extra properties configured on the KB source.

**Request body**

```json
{
  "id": "<document-id>"
}
```

| Field | Type   | Required | Description      |
| ----- | ------ | -------- | ---------------- |
| `id`  | string | no       | The document ID. |

**Response**

```json
{
  "response": {
    "author": "string",
    "department": "string",
    "classification": "string"
  }
}
```

Returns a dictionary of available metadata field names and their types.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/document/kb-meta-fields" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "doc_abc123"}'
```

***

### POST /api/document/parsing-blocks

Retrieve the parsed content blocks (chunks) produced by the file parser for a document. Supports pagination.

**Request body**

```json
{
  "id": "<document-id>",
  "offset": 0,
  "limit": 20
}
```

| Field    | Type    | Required | Default | Description                         |
| -------- | ------- | -------- | ------- | ----------------------------------- |
| `id`     | string  | no       | —       | The document ID.                    |
| `offset` | integer | no       | `0`     | Pagination offset.                  |
| `limit`  | integer | no       | `20`    | Maximum number of blocks to return. |

**Response**

```json
{
  "response": [
    {
      "id": "<block-id>",
      "content": "The regulation specifies that..."
    }
  ]
}
```

Each block contains an `id` and its text `content`.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/document/parsing-blocks" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "doc_abc123", "offset": 0, "limit": 20}'
```
