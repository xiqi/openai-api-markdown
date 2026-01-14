# Create vector store file

Source: https://platform.openai.com/docs/api-reference/vector-stores-files/createFile

`POST /v1/vector_stores/{vector_store_id}/files`

Create a vector store file by attaching a [File](../files/index.md) to a [vector store](../vector-stores/object.md).

## Parameters
- `vector_store_id` (path, string, required): The ID of the vector store for which to create a File.

## Request body
### application/json
- `file_id` (string, required): A [File](../files/index.md) ID that the vector store should use. Useful for tools like `file_search` that can access files.
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
- `object` (string, required): The object type, which is always `vector_store.file`. Enum: 'vector_store.file'.
- `usage_bytes` (integer, required): The total vector store usage in bytes. Note that this may be different from the original file size.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the vector store file was created.
- `vector_store_id` (string, required): The ID of the [vector store](../vector-stores/object.md) that the [File](../files/index.md) is attached to.
- `status` (string, required): The status of the vector store file, which can be either `in_progress`, `completed`, `cancelled`, or `failed`. The status `completed` indicates that the vector store file is ready for use. Enum: 'in_progress', 'completed', 'cancelled', 'failed'.
- `last_error` (object | null, required)
  - Variant (object):
    - `code` (string, required): One of `server_error`, `unsupported_file`, or `invalid_file`. Enum: 'server_error', 'unsupported_file', 'invalid_file'.
    - `message` (string, required): A human-readable description of the error.
- `chunking_strategy` (object, optional): The strategy used to chunk the file.
  - Variant (object):
    - `type` (string, required): Always `static`. Enum: 'static'.
    - `static` (object, required)
      - `max_chunk_size_tokens` (integer, required): The maximum number of tokens in each chunk. The default value is `800`. The minimum value is `100` and the maximum value is `4096`.
      - `chunk_overlap_tokens` (integer, required): The number of tokens that overlap between chunks. The default value is `400`.
        
        Note that the overlap must not exceed half of `max_chunk_size_tokens`.
  - Variant (object):
    - `type` (string, required): Always `other`. Enum: 'other'.
- `attributes` (object | null, optional)

## Returns
A [vector store file](file-object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/vector_stores/vs_abc123/files \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -H "Content-Type: application/json" \
    -H "OpenAI-Beta: assistants=v2" \
    -d '{
      "file_id": "file-abc123"
    }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

vector_store_file = client.vector_stores.files.create(
  vector_store_id="vs_abc123",
  file_id="file-abc123"
)
print(vector_store_file)
```
#### Response
```json
{
  "id": "file-abc123",
  "object": "vector_store.file",
  "created_at": 1699061776,
  "usage_bytes": 1234,
  "vector_store_id": "vs_abcd",
  "status": "completed",
  "last_error": null
}
```
