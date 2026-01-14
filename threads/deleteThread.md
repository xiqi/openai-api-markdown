# Delete thread

Source: https://platform.openai.com/docs/api-reference/threads/deleteThread

`DELETE /v1/threads/{thread_id}`

Delete a thread.

## Parameters
- `thread_id` (path, string, required): The ID of the thread to delete.

## Responses
### 200
OK
#### application/json
- `id` (string, required)
- `deleted` (boolean, required)
- `object` (string, required) Enum: 'thread.deleted'.

## Returns
Deletion status

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/threads/thread_abc123 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Beta: assistants=v2" \
  -X DELETE
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

response = client.beta.threads.delete("thread_abc123")
print(response)
```
#### Response
```json
{
  "id": "thread_abc123",
  "object": "thread.deleted",
  "deleted": true
}
```
