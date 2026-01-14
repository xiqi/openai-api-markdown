# Retrieve thread

Source: https://platform.openai.com/docs/api-reference/threads/getThread

`GET /v1/threads/{thread_id}`

Retrieves a thread.

## Parameters
- `thread_id` (path, string, required): The ID of the thread to retrieve.

## Responses
### 200
OK
#### application/json
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `thread`. Enum: 'thread'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the thread was created.
- `tool_resources` (object | null, required)
  - Variant (object):
    - `code_interpreter` (object, optional)
      - `file_ids` (array<string>, optional): A list of [file](../files/index.md) IDs made available to the `code_interpreter` tool. There can be a maximum of 20 files associated with the tool. Default: `[]`.
    - `file_search` (object, optional)
      - `vector_store_ids` (array<string>, optional): The [vector store](../vector-stores/object.md) attached to this thread. There can be a maximum of 1 vector store attached to the thread.
- `metadata` (object | null, required)

## Returns
The [thread](object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/threads/thread_abc123 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Beta: assistants=v2"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

my_thread = client.beta.threads.retrieve("thread_abc123")
print(my_thread)
```
#### Response
```json
{
  "id": "thread_abc123",
  "object": "thread",
  "created_at": 1699014083,
  "metadata": {},
  "tool_resources": {
    "code_interpreter": {
      "file_ids": []
    }
  }
}
```
