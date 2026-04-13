---
description: >-
  The Semantic Graph endpoints expose the knowledge graph built from indexed
  documents: nodes, relationships, and exploration primitives.
---

# Semantic graph

_Authenticated with `instance-id` + `api-key` headers — see Instance API keys._

***

### POST /api/semantic-graph/identify-nodes

Identify all semantic nodes relevant to a query. The system translates the query, embeds it, finds approximate related nodes, then uses an LLM to select the most relevant documents. If `need_documents` is `true`, partial document content involved by the nodes is included in the response; otherwise only document IDs are returned.

**Request body**

```json
{
  "query": "What are the safety requirements?",
  "need_documents": false
}
```

| Field            | Type    | Required | Default | Description                                                  |
| ---------------- | ------- | -------- | ------- | ------------------------------------------------------------ |
| `query`          | string  | no       | `null`  | The natural-language query to match against the graph.       |
| `need_documents` | boolean | no       | `false` | If `true`, include partial document content in the response. |

**Response**

```json
{
  "response": {
    "semantic_nodes": [
      {
        "node_1": "Safety regulation",
        "node_2": "Fire prevention",
        "edge": "requires",
        "documents": ["doc_abc123", "doc_def456"]
      }
    ],
    "documents_contents": [
      {
        "document_id": "doc_abc123",
        "content": ["Section 4.2 specifies that...", "The regulation mandates..."]
      }
    ]
  }
}
```

| Field                | Type  | Description                                                                                         |
| -------------------- | ----- | --------------------------------------------------------------------------------------------------- |
| `semantic_nodes`     | array | Matched graph triples (`node_1`, `node_2`, `edge`) with associated document IDs.                    |
| `documents_contents` | array | Partial document content for each involved document (only present when `need_documents` is `true`). |

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/semantic-graph/identify-nodes" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"query": "What are the safety requirements?", "need_documents": true}'
```

***

### POST /api/semantic-graph/nodes

List all semantic nodes in the instance with pagination.

**Request body**

```json
{
  "offset": 0,
  "limit": 50
}
```

| Field    | Type    | Required | Default | Description                        |
| -------- | ------- | -------- | ------- | ---------------------------------- |
| `offset` | integer | no       | `0`     | Pagination offset.                 |
| `limit`  | integer | no       | `50`    | Maximum number of nodes to return. |

**Response**

```json
{
  "response": [
    {
      "id": "<node-id>",
      "node_1": "Safety regulation",
      "node_2": "Fire prevention",
      "edge": "requires",
      "extraproperties": { }
    }
  ]
}
```

Each node contains `id`, `node_1` (source entity), `node_2` (target entity), `edge` (relationship label), and `extraproperties` (additional metadata).

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/semantic-graph/nodes" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"offset": 0, "limit": 50}'
```

***

### POST /api/semantic-graph/nodes-by-label

List semantic nodes by label. A label corresponds to the value of `node_1` or `node_2` in a semantic node — this endpoint finds all nodes where either entity matches the given label.

**Request body**

```json
{
  "label": "Safety regulation",
  "limit": 20,
  "offset": 0
}
```

| Field    | Type    | Required | Default | Description                                             |
| -------- | ------- | -------- | ------- | ------------------------------------------------------- |
| `label`  | string  | no       | `""`    | The entity label to search for in `node_1` or `node_2`. |
| `limit`  | integer | no       | `20`    | Maximum number of nodes to return.                      |
| `offset` | integer | no       | `0`     | Pagination offset.                                      |

**Response**

```json
{
  "response": [
    {
      "id": "<node-id>",
      "node_1": "Safety regulation",
      "node_2": "Fire prevention",
      "edge": "requires",
      "extraproperties": { }
    }
  ]
}
```

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/semantic-graph/nodes-by-label" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"label": "Safety regulation", "limit": 20, "offset": 0}'
```

***

### POST /api/semantic-graph/linked-nodes-by-id

Find nodes similar to (sharing labels with) the `node_1` or `node_2` of a given semantic node. This enables graph exploration by following connections from a known node.

**Request body**

```json
{
  "id": "<node-id>"
}
```

| Field | Type   | Required | Description                                           |
| ----- | ------ | -------- | ----------------------------------------------------- |
| `id`  | string | yes      | The ID of the semantic node to find linked nodes for. |

**Response**

```json
{
  "response": [
    {
      "id": "<node-id>",
      "node_1": "Fire prevention",
      "node_2": "Emergency exits",
      "edge": "includes",
      "extraproperties": { }
    }
  ]
}
```

Returns a list of semantic nodes that share entity labels with the specified node.

**Example**

```bash
curl -X POST "https://api.kai-studio.ai/api/semantic-graph/linked-nodes-by-id" \
  -H "instance-id: <your-instance-id>" \
  -H "api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"id": "node_xyz789"}'
```
