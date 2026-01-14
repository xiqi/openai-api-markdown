# Cancel vector store file batch

Source: https://platform.openai.com/docs/api-reference/vector-stores-file-batches/cancelBatch

`POST /v1/vector_stores/{vector_store_id}/file_batches/{batch_id}/cancel`

Cancel a vector store file batch. This attempts to cancel the processing of files in this batch as soon as possible.

## Parameters
- `vector_store_id` (path, string, required): The ID of the vector store that the file batch belongs to.
- `batch_id` (path, string, required): The ID of the file batch to cancel.

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
The modified vector store file batch object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/vector_stores/vs_abc123/files_batches/vsfb_abc123/cancel \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2" \
  -X POST
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

deleted_vector_store_file_batch = client.vector_stores.file_batches.cancel(
    vector_store_id="vs_abc123",
    file_batch_id="vsfb_abc123"
)
print(deleted_vector_store_file_batch)
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
    "in_progress": 12,
    "completed": 3,
    "failed": 0,
    "cancelled": 0,
    "total": 15,
  }
}
```
