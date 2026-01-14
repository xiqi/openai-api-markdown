# Delete ChatKit thread

Source: https://platform.openai.com/docs/api-reference/chatkit/threads/delete

`DELETE /v1/chatkit/threads/{thread_id}`

Delete a ChatKit thread

## Parameters
- `thread_id` (path, string, required): Identifier of the ChatKit thread to delete.

## Responses
### 200
Success
#### application/json
- `id` (string, required): Identifier of the deleted thread.
- `object` (string, required): Type discriminator that is always `chatkit.thread.deleted`. Enum: 'chatkit.thread.deleted'. Default: `chatkit.thread.deleted`.
- `deleted` (boolean, required): Indicates that the thread has been deleted.

## Returns
Returns a confirmation object for the deleted thread.

## Examples
### Example
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
thread = client.beta.chat_kit.threads.delete(
    "cthr_123",
)
print(thread.id)
```
