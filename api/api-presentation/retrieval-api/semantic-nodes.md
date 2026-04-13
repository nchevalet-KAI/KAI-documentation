# Semantic nodes

Search the semantic graph of documents across instances the user can access. **This endpoint replaces the removed `/search` from the KAI Instance API** — see Removed endpoints and Why MCP.

_Authenticated with an OAuth 2.1 Bearer token or the `kai_auth` cookie — see OAuth 2.1._

***

### POST /retrieval/semantic-nodes/search

Performs a semantic search in a specific knowledge base to find relevant documents, procedures, policies, and references. Returns document excerpts with their content. The `instance_id` parameter must come from `list-available-instances`.

Unlike the old `/search` endpoint, this does **not** call an LLM server-side. It returns raw semantic nodes and document content, letting your LLM client synthesise the answer with full control over the prompt and model.

**Request body**

```json
{
  "query": "What are the safety requirements for electrical installations?",
  "instance_id": "inst_abc123"
}
```

| Field         | Type  | Required | Description                                                     |
| ------------- | ----- | -------- | --------------------------------------------------------------- |
| `query`       | `str` | Yes      | The natural-language search query.                              |
| `instance_id` | `str` | Yes      | ID of the instance to search (from `list-available-instances`). |

**Response**

```json
{
  "response": {
    "semantic_nodes": [ "..." ],
    "documents_contents": [ "..." ]
  }
}
```

The response contains matched semantic nodes and the content of the documents they belong to.

| Field                | Type   | Description                                                            |
| -------------------- | ------ | ---------------------------------------------------------------------- |
| `semantic_nodes`     | `list` | Semantic graph nodes matching the query, with relevance metadata.      |
| `documents_contents` | `list` | Content excerpts from the documents associated with the matched nodes. |

**Example**

```bash
curl -X POST "https://api-retrieval.kai-studio.ai/retrieval/semantic-nodes/search" \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "What are the safety requirements for electrical installations?",
    "instance_id": "inst_abc123"
  }'
```
