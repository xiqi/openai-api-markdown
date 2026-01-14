# List vector store files

Source: https://platform.openai.com/docs/api-reference/vector-stores-files/listFiles

`GET /v1/vector_stores/{vector_store_id}/files`

Returns a list of vector store files.

## Parameters
- `vector_store_id` (path, string, required): The ID of the vector store that the files belong to.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `order` (query, string, optional): Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and `desc` for descending order. Enum: 'asc', 'desc'. Default: `desc`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `before` (query, string, optional): A cursor for use in pagination. `before` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, starting with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list.
- `filter` (query, string, optional): Filter by file status. One of `in_progress`, `completed`, `failed`, `cancelled`. Enum: 'in_progress', 'completed', 'failed', 'cancelled'.

## Responses
### 200
OK
#### application/json
- `object` (string, required)
- `data` (array<object>, required)
  - Items:
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
          - ...
      - Variant (object):
        - `type` (string, required): Always `other`. Enum: 'other'.
    - `attributes` (object | null, optional)
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [vector store file](file-object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/vector_stores/vs_abc123/files \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

vector_store_files = client.vector_stores.files.list(
  vector_store_id="vs_abc123"
)
print(vector_store_files)
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "id": "file-abc123",
      "object": "vector_store.file",
      "created_at": 1699061776,
      "vector_store_id": "vs_abc123"
    },
    {
      "id": "file-abc456",
      "object": "vector_store.file",
      "created_at": 1699061776,
      "vector_store_id": "vs_abc123"
    }
  ],
  "first_id": "file-abc123",
  "last_id": "file-abc456",
  "has_more": false
}
```
