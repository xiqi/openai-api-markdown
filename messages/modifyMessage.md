# Modify message

Source: https://platform.openai.com/docs/api-reference/messages/modifyMessage

`POST /v1/threads/{thread_id}/messages/{message_id}`

Modifies a message.

## Parameters
- `thread_id` (path, string, required): The ID of the thread to which this message belongs.
- `message_id` (path, string, required): The ID of the message to modify.

## Request body
### application/json
- `metadata` (object | null, optional)

## Responses
### 200
OK
#### application/json
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `thread.message`. Enum: 'thread.message'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the message was created.
- `thread_id` (string, required): The [thread](../threads/index.md) ID that this message belongs to.
- `status` (string, required): The status of the message, which can be either `in_progress`, `incomplete`, or `completed`. Enum: 'in_progress', 'incomplete', 'completed'.
- `incomplete_details` (object | null, required)
  - Variant (object):
    - `reason` (string, required): The reason the message is incomplete. Enum: 'content_filter', 'max_tokens', 'run_cancelled', 'run_expired', 'run_failed'.
- `completed_at` (integer | null, required)
- `incomplete_at` (integer | null, required)
- `role` (string, required): The entity that produced the message. One of `user` or `assistant`. Enum: 'user', 'assistant'.
- `content` (array<object>, required): The content of the message in array of text and/or images.
- `assistant_id` (string | null, required)
- `run_id` (string | null, required)
- `attachments` (array<object> | null, required)
- `metadata` (object | null, required)

## Returns
The modified [message](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/threads/thread_abc123/messages/msg_abc123 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Beta: assistants=v2" \
  -d '{
      "metadata": {
        "modified": "true",
        "user": "abc123"
      }
    }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

message = client.beta.threads.messages.update(
  message_id="msg_abc12",
  thread_id="thread_abc123",
  metadata={
    "modified": "true",
    "user": "abc123",
  },
)
print(message)
```
#### Response
```json
{
  "id": "msg_abc123",
  "object": "thread.message",
  "created_at": 1699017614,
  "assistant_id": null,
  "thread_id": "thread_abc123",
  "run_id": null,
  "role": "user",
  "content": [
    {
      "type": "text",
      "text": {
        "value": "How does AI work? Explain it in simple terms.",
        "annotations": []
      }
    }
  ],
  "file_ids": [],
  "metadata": {
    "modified": "true",
    "user": "abc123"
  }
}
```
