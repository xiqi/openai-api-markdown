# List vector stores

Source: https://platform.openai.com/docs/api-reference/vector-stores/list

`GET /v1/vector_stores`

Returns a list of vector stores.

## Parameters
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `order` (query, string, optional): Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and `desc` for descending order. Enum: 'asc', 'desc'. Default: `desc`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `before` (query, string, optional): A cursor for use in pagination. `before` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, starting with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list.

## Responses
### 200
OK
#### application/json
- `object` (string, required)
- `data` (array<object>, required)
  - Items:
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
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [vector store](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/vector_stores \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

vector_stores = client.vector_stores.list()
print(vector_stores)
```
#### Response
```json
{
  "object": "list",
  "data": [
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
    },
    {
      "id": "vs_abc456",
      "object": "vector_store",
      "created_at": 1699061776,
      "name": "Support FAQ v2",
      "description": null,
      "bytes": 139920,
      "file_counts": {
        "in_progress": 0,
        "completed": 3,
        "failed": 0,
        "cancelled": 0,
        "total": 3
      }
    }
  ],
  "first_id": "vs_abc123",
  "last_id": "vs_abc456",
  "has_more": false
}
```
