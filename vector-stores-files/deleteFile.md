# Delete vector store file

Source: https://platform.openai.com/docs/api-reference/vector-stores-files/deleteFile

`DELETE /v1/vector_stores/{vector_store_id}/files/{file_id}`

Delete a vector store file. This will remove the file from the vector store but the file itself will not be deleted. To delete the file, use the [delete file](../files/delete.md) endpoint.

## Parameters
- `vector_store_id` (path, string, required): The ID of the vector store that the file belongs to.
- `file_id` (path, string, required): The ID of the file to delete.

## Responses
### 200
OK
#### application/json
- `id` (string, required)
- `deleted` (boolean, required)
- `object` (string, required) Enum: 'vector_store.file.deleted'.

## Returns
Deletion status

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/vector_stores/vs_abc123/files/file-abc123 \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2" \
  -X DELETE
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

deleted_vector_store_file = client.vector_stores.files.delete(
    vector_store_id="vs_abc123",
    file_id="file-abc123"
)
print(deleted_vector_store_file)
```
#### Response
```json
{
  id: "file-abc123",
  object: "vector_store.file.deleted",
  deleted: true
}
```
