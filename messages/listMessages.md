# List messages

Source: https://platform.openai.com/docs/api-reference/messages/listMessages

`GET /v1/threads/{thread_id}/messages`

Returns a list of messages for a given thread.

## Parameters
- `thread_id` (path, string, required): The ID of the [thread](../threads/index.md) the messages belong to.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `order` (query, string, optional): Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and `desc` for descending order. Enum: 'asc', 'desc'. Default: `desc`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `before` (query, string, optional): A cursor for use in pagination. `before` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, starting with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list.
- `run_id` (query, string, optional): Filter messages by the run ID that generated them.

## Responses
### 200
OK
#### application/json
- `object` (string, required)
- `data` (array<object>, required)
  - Items:
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
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [message](index.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/threads/thread_abc123/messages \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Beta: assistants=v2"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

thread_messages = client.beta.threads.messages.list("thread_abc123")
print(thread_messages.data)
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "id": "msg_abc123",
      "object": "thread.message",
      "created_at": 1699016383,
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
      "attachments": [],
      "metadata": {}
    },
    {
      "id": "msg_abc456",
      "object": "thread.message",
      "created_at": 1699016383,
      "assistant_id": null,
      "thread_id": "thread_abc123",
      "run_id": null,
      "role": "user",
      "content": [
        {
          "type": "text",
          "text": {
            "value": "Hello, what is AI?",
            "annotations": []
          }
        }
      ],
      "attachments": [],
      "metadata": {}
    }
  ],
  "first_id": "msg_abc123",
  "last_id": "msg_abc456",
  "has_more": false
}
```
