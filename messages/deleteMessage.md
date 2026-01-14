# Delete message

Source: https://platform.openai.com/docs/api-reference/messages/deleteMessage

`DELETE /v1/threads/{thread_id}/messages/{message_id}`

Deletes a message.

## Parameters
- `thread_id` (path, string, required): The ID of the thread to which this message belongs.
- `message_id` (path, string, required): The ID of the message to delete.

## Responses
### 200
OK
#### application/json
- `id` (string, required)
- `deleted` (boolean, required)
- `object` (string, required) Enum: 'thread.message.deleted'.

## Returns
Deletion status

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/threads/thread_abc123/messages/msg_abc123 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Beta: assistants=v2"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

deleted_message = client.beta.threads.messages.delete(
  message_id="msg_abc12",
  thread_id="thread_abc123",
)
print(deleted_message)
```
#### Response
```json
{
  "id": "msg_abc123",
  "object": "thread.message.deleted",
  "deleted": true
}
```
