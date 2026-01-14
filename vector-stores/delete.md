# Delete vector store

Source: https://platform.openai.com/docs/api-reference/vector-stores/delete

`DELETE /v1/vector_stores/{vector_store_id}`

Delete a vector store.

## Parameters
- `vector_store_id` (path, string, required): The ID of the vector store to delete.

## Responses
### 200
OK
#### application/json
- `id` (string, required)
- `deleted` (boolean, required)
- `object` (string, required) Enum: 'vector_store.deleted'.

## Returns
Deletion status

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/vector_stores/vs_abc123 \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2" \
  -X DELETE
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

deleted_vector_store = client.vector_stores.delete(
  vector_store_id="vs_abc123"
)
print(deleted_vector_store)
```
#### Response
```json
{
  id: "vs_abc123",
  object: "vector_store.deleted",
  deleted: true
}
```
