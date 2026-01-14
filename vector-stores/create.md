# Create vector store

Source: https://platform.openai.com/docs/api-reference/vector-stores/create

`POST /v1/vector_stores`

Create a vector store.

## Request body
### application/json
- `file_ids` (array<string>, optional): A list of [File](../files/index.md) IDs that the vector store should use. Useful for tools like `file_search` that can access files.
- `name` (string, optional): The name of the vector store.
- `description` (string, optional): A description for the vector store. Can be used to describe the vector store's purpose.
- `expires_after` (object, optional): The expiration policy for a vector store.
  - `anchor` (string, required): Anchor timestamp after which the expiration policy applies. Supported anchors: `last_active_at`. Enum: 'last_active_at'.
  - `days` (integer, required): The number of days after the anchor time that the vector store will expire.
- `chunking_strategy` (object, optional): The chunking strategy used to chunk the file(s). If not set, will use the `auto` strategy. Only applicable if `file_ids` is non-empty.
  - Variant (object):
    - `type` (string, required): Always `auto`. Enum: 'auto'.
  - Variant (object):
    - `type` (string, required): Always `static`. Enum: 'static'.
    - `static` (object, required)
      - `max_chunk_size_tokens` (integer, required): The maximum number of tokens in each chunk. The default value is `800`. The minimum value is `100` and the maximum value is `4096`.
      - `chunk_overlap_tokens` (integer, required): The number of tokens that overlap between chunks. The default value is `400`.
        
        Note that the overlap must not exceed half of `max_chunk_size_tokens`.
- `metadata` (object | null, optional)

## Responses
### 200
OK
#### application/json
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `vector_store`. Enum: 'vector_store'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the vector store was created.
- `name` (string, required): The name of the vector store.
- `usage_bytes` (integer, required): The total number of bytes used by the files in the vector store.
- `file_counts` (object, required)
  - `in_progress` (integer, required): The number of files that are currently being processed.
  - `completed` (integer, required): The number of files that have been successfully processed.
  - `failed` (integer, required): The number of files that have failed to process.
  - `cancelled` (integer, required): The number of files that were cancelled.
  - `total` (integer, required): The total number of files.
- `status` (string, required): The status of the vector store, which can be either `expired`, `in_progress`, or `completed`. A status of `completed` indicates that the vector store is ready for use. Enum: 'expired', 'in_progress', 'completed'.
- `expires_after` (object, optional): The expiration policy for a vector store.
  - `anchor` (string, required): Anchor timestamp after which the expiration policy applies. Supported anchors: `last_active_at`. Enum: 'last_active_at'.
  - `days` (integer, required): The number of days after the anchor time that the vector store will expire.
- `expires_at` (integer | null, optional)
- `last_active_at` (integer | null, required)
- `metadata` (object | null, required)

## Returns
A [vector store](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/vector_stores \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2" \
  -d '{
    "name": "Support FAQ"
  }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

vector_store = client.vector_stores.create(
  name="Support FAQ"
)
print(vector_store)
```
#### Response
```json
{
  "id": "vs_abc123",
  "object": "vector_store",
  "created_at": 1699061776,
  "name": "Support FAQ",
  "description": "Contains commonly asked questions and answers, organized by topic.",
  "bytes": 139920,
  "file_counts": {
    "in_progress": 0,
    "completed": 3,
    "failed": 0,
    "cancelled": 0,
    "total": 3
  }
}
```
