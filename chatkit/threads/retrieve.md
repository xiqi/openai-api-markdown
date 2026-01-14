# Retrieve ChatKit thread

Source: https://platform.openai.com/docs/api-reference/chatkit/threads/retrieve

`GET /v1/chatkit/threads/{thread_id}`

Retrieve a ChatKit thread

## Parameters
- `thread_id` (path, string, required): Identifier of the ChatKit thread to retrieve.

## Responses
### 200
Success
#### application/json
- `id` (string, required): Identifier of the thread.
- `object` (string, required): Type discriminator that is always `chatkit.thread`. Enum: 'chatkit.thread'. Default: `chatkit.thread`.
- `created_at` (integer, required): Unix timestamp (in seconds) for when the thread was created.
- `title` (string | null, required)
- `status` (object, required): Current status for the thread. Defaults to `active` for newly created threads.
  - Variant (object):
    - `type` (string, required): Status discriminator that is always `active`. Enum: 'active'. Default: `active`.
  - Variant (object):
    - `type` (string, required): Status discriminator that is always `locked`. Enum: 'locked'. Default: `locked`.
    - `reason` (string | null, required)
  - Variant (object):
    - `type` (string, required): Status discriminator that is always `closed`. Enum: 'closed'. Default: `closed`.
    - `reason` (string | null, required)
- `user` (string, required): Free-form string that identifies your end user who owns the thread.

Example:
```json
{
  "id": "cthr_def456",
  "object": "chatkit.thread",
  "created_at": 1712345600,
  "title": "Demo feedback",
  "status": {
    "type": "active"
  },
  "user": "user_456"
}
```

## Returns
Returns a [Thread](object.md) object.

## Examples
### Retrieve a thread by ID
#### Request (curl)
```bash
curl https://api.openai.com/v1/chatkit/threads/cthr_abc123 \
  -H "OpenAI-Beta: chatkit_beta=v1" \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from 'openai';

const client = new OpenAI();

const chatkitThread = await client.beta.chatkit.threads.retrieve('cthr_123');

console.log(chatkitThread.id);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
chatkit_thread = client.beta.chatkit.threads.retrieve(
    "cthr_123",
)
print(chatkit_thread.id)
```
#### Response
```json
{
  "id": "cthr_abc123",
  "object": "chatkit.thread",
  "title": "Customer escalation",
  "items": {
    "data": [
      {
        "id": "cthi_user_001",
        "object": "chatkit.thread_item",
        "type": "user_message",
        "content": [
          {
            "type": "input_text",
            "text": "I need help debugging an onboarding issue."
          }
        ],
        "attachments": []
      },
      {
        "id": "cthi_assistant_002",
        "object": "chatkit.thread_item",
        "type": "assistant_message",
        "content": [
          {
            "type": "output_text",
            "text": "Let's start by confirming the workflow version you deployed."
          }
        ]
      }
    ],
    "has_more": false
  }
}
```
