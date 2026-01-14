# Create vector store file batch

Source: https://platform.openai.com/docs/api-reference/vector-stores-file-batches/createBatch

`POST /v1/vector_stores/{vector_store_id}/file_batches`

Create a vector store file batch.

## Parameters
- `vector_store_id` (path, string, required): The ID of the vector store for which to create a File Batch.

## Request body
### application/json
- `file_ids` (array<string>, optional): A list of [File](../files/index.md) IDs that the vector store should use. Useful for tools like `file_search` that can access files.  If `attributes` or `chunking_strategy` are provided, they will be  applied to all files in the batch. Mutually exclusive with `files`.
- `files` (array<object>, optional): A list of objects that each include a `file_id` plus optional `attributes` or `chunking_strategy`. Use this when you need to override metadata for specific files. The global `attributes` or `chunking_strategy` will be ignored and must be specified for each file. Mutually exclusive with `file_ids`.
  - Items:
    - `file_id` (string, required): A [File](../files/index.md) ID that the vector store should use. Useful for tools like `file_search` that can access files.
    - `chunking_strategy` (object, optional): The chunking strategy used to chunk the file(s). If not set, will use the `auto` strategy.
      - Variant (object):
        - `type` (string, required): Always `auto`. Enum: 'auto'.
      - Variant (object):
        - `type` (string, required): Always `static`. Enum: 'static'.
        - `static` (object, required)
          - ...
    - `attributes` (object | null, optional)
- `chunking_strategy` (object, optional): The chunking strategy used to chunk the file(s). If not set, will use the `auto` strategy.
  - Variant (object):
    - `type` (string, required): Always `auto`. Enum: 'auto'.
  - Variant (object):
    - `type` (string, required): Always `static`. Enum: 'static'.
    - `static` (object, required)
      - `max_chunk_size_tokens` (integer, required): The maximum number of tokens in each chunk. The default value is `800`. The minimum value is `100` and the maximum value is `4096`.
      - `chunk_overlap_tokens` (integer, required): The number of tokens that overlap between chunks. The default value is `400`.
        
        Note that the overlap must not exceed half of `max_chunk_size_tokens`.
- `attributes` (object | null, optional)

## Responses
### 200
OK
#### application/json
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `vector_store.file_batch`. Enum: 'vector_store.files_batch'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the vector store files batch was created.
- `vector_store_id` (string, required): The ID of the [vector store](../vector-stores/object.md) that the [File](../files/index.md) is attached to.
- `status` (string, required): The status of the vector store files batch, which can be either `in_progress`, `completed`, `cancelled` or `failed`. Enum: 'in_progress', 'completed', 'cancelled', 'failed'.
- `file_counts` (object, required)
  - `in_progress` (integer, required): The number of files that are currently being processed.
  - `completed` (integer, required): The number of files that have been processed.
  - `failed` (integer, required): The number of files that have failed to process.
  - `cancelled` (integer, required): The number of files that where cancelled.
  - `total` (integer, required): The total number of files.

## Returns
A [vector store file batch](batch-object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/vector_stores/vs_abc123/file_batches \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -H "Content-Type: application/json \
    -H "OpenAI-Beta: assistants=v2" \
    -d '{
      "files": [
        {
          "file_id": "file-abc123",
          "attributes": {"category": "finance"}
        },
        {
          "file_id": "file-abc456",
          "chunking_strategy": {
            "type": "static",
            "max_chunk_size_tokens": 1200,
            "chunk_overlap_tokens": 200
          }
        }
      ]
    }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

vector_store_file_batch = client.vector_stores.file_batches.create(
  vector_store_id="vs_abc123",
  files=[
    {
      "file_id": "file-abc123",
      "attributes": {"category": "finance"},
    },
    {
      "file_id": "file-abc456",
      "chunking_strategy": {
        "type": "static",
        "max_chunk_size_tokens": 1200,
        "chunk_overlap_tokens": 200,
      },
    },
  ],
)
print(vector_store_file_batch)
```
#### Response
```json
{
  "id": "vsfb_abc123",
  "object": "vector_store.file_batch",
  "created_at": 1699061776,
  "vector_store_id": "vs_abc123",
  "status": "in_progress",
  "file_counts": {
    "in_progress": 1,
    "completed": 1,
    "failed": 0,
    "cancelled": 0,
    "total": 0,
  }
}
```
