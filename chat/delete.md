# Delete chat completion

Source: https://platform.openai.com/docs/api-reference/chat/delete

`DELETE /v1/chat/completions/{completion_id}`

Delete a stored chat completion. Only Chat Completions that have been
created with the `store` parameter set to `true` can be deleted.

## Parameters
- `completion_id` (path, string, required): The ID of the chat completion to delete.

## Responses
### 200
The chat completion was deleted successfully.
#### application/json
- `object` (string, required): The type of object being deleted. Enum: 'chat.completion.deleted'.
- `id` (string, required): The ID of the chat completion that was deleted.
- `deleted` (boolean, required): Whether the chat completion was deleted.

## Returns
A deletion confirmation object.

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/chat/completions/chat_abc123 \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

completions = client.chat.completions.list()
first_id = completions[0].id
delete_response = client.chat.completions.delete(completion_id=first_id)
print(delete_response)
```
#### Response
```json
{
  "object": "chat.completion.deleted",
  "id": "chatcmpl-AyPNinnUqUDYo9SAdA52NobMflmj2",
  "deleted": true
}
```
