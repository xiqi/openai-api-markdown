# Search vector store

Source: https://platform.openai.com/docs/api-reference/vector-stores/search

`POST /v1/vector_stores/{vector_store_id}/search`

Search a vector store for relevant chunks based on a query and file attributes filter.

## Parameters
- `vector_store_id` (path, string, required): The ID of the vector store to search.

## Request body
### application/json
- `query` (string | array<string>, required): A query string for a search
- `rewrite_query` (boolean, optional): Whether to rewrite the natural language query for vector search. Default: `False`.
- `max_num_results` (integer, optional): The maximum number of results to return. This number should be between 1 and 50 inclusive. Default: `10`.
- `filters` (object, optional): A filter to apply based on file attributes.
  - Variant (object):
    - `type` (string, required): Specifies the comparison operator: `eq`, `ne`, `gt`, `gte`, `lt`, `lte`, `in`, `nin`.
      - `eq`: equals
      - `ne`: not equal
      - `gt`: greater than
      - `gte`: greater than or equal
      - `lt`: less than
      - `lte`: less than or equal
      - `in`: in
      - `nin`: not in Enum: 'eq', 'ne', 'gt', 'gte', 'lt', 'lte'. Default: `eq`.
    - `key` (string, required): The key to compare against the value.
    - `value` (string | number | boolean | array<string | number>, required): The value to compare against the attribute key; supports string, number, or boolean types.
  - Variant (object):
    - `type` (string, required): Type of operation: `and` or `or`. Enum: 'and', 'or'.
    - `filters` (array<object>, required): Array of filters to combine. Items can be `ComparisonFilter` or `CompoundFilter`.
- `ranking_options` (object, optional): Ranking options for search.
  - `ranker` (string, optional): Enable re-ranking; set to `none` to disable, which can help reduce latency. Enum: 'none', 'auto', 'default-2024-11-15'. Default: `auto`.
  - `score_threshold` (number, optional) Default: `0`.

## Responses
### 200
OK
#### application/json
- `object` (string, required): The object type, which is always `vector_store.search_results.page` Enum: 'vector_store.search_results.page'.
- `search_query` (array<string>, required)
- `data` (array<object>, required): The list of search result items.
  - Items:
    - `file_id` (string, required): The ID of the vector store file.
    - `filename` (string, required): The name of the vector store file.
    - `score` (number, required): The similarity score for the result.
    - `attributes` (object | null, required)
    - `content` (array<object>, required): Content chunks from the file.
      - Items:
        - `type` (string, required): The type of content. Enum: 'text'.
        - `text` (string, required): The text content returned from search.
- `has_more` (boolean, required): Indicates if there are more results to fetch.
- `next_page` (string | null, required)

## Returns
A page of search results from the vector store.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST \
https://api.openai.com/v1/vector_stores/vs_abc123/search \
-H "Authorization: Bearer $OPENAI_API_KEY" \
-H "Content-Type: application/json" \
-d '{"query": "What is the return policy?", "filters": {...}}'
```
#### Response
```json
{
  "object": "vector_store.search_results.page",
  "search_query": "What is the return policy?",
  "data": [
    {
      "file_id": "file_123",
      "filename": "document.pdf",
      "score": 0.95,
      "attributes": {
        "author": "John Doe",
        "date": "2023-01-01"
      },
      "content": [
        {
          "type": "text",
          "text": "Relevant chunk"
        }
      ]
    },
    {
      "file_id": "file_456",
      "filename": "notes.txt",
      "score": 0.89,
      "attributes": {
        "author": "Jane Smith",
        "date": "2023-01-02"
      },
      "content": [
        {
          "type": "text",
          "text": "Sample text content from the vector store."
        }
      ]
    }
  ],
  "has_more": false,
  "next_page": null
}
```
