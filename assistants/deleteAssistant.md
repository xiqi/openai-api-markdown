# Delete assistant

Source: https://platform.openai.com/docs/api-reference/assistants/deleteAssistant

`DELETE /v1/assistants/{assistant_id}`

Delete an assistant.

## Parameters
- `assistant_id` (path, string, required): The ID of the assistant to delete.

## Responses
### 200
OK
#### application/json
- `id` (string, required)
- `deleted` (boolean, required)
- `object` (string, required) Enum: 'assistant.deleted'.

## Returns
Deletion status

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/assistants/asst_abc123 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Beta: assistants=v2" \
  -X DELETE
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

response = client.beta.assistants.delete("asst_abc123")
print(response)
```
#### Response
```json
{
  "id": "asst_abc123",
  "object": "assistant.deleted",
  "deleted": true
}
```
