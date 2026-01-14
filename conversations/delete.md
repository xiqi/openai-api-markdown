# Delete a conversation

Source: https://platform.openai.com/docs/api-reference/conversations/delete

`DELETE /v1/conversations/{conversation_id}`

Delete a conversation. Items in the conversation will not be deleted.

## Parameters
- `conversation_id` (path, string, required): The ID of the conversation to delete.

## Responses
### 200
Success
#### application/json
- `object` (string, required) Enum: 'conversation.deleted'. Default: `conversation.deleted`.
- `deleted` (boolean, required)
- `id` (string, required)

## Returns
A success message.

## Examples
### Delete a conversation
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/conversations/conv_123 \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const deleted = await client.conversations.delete("conv_123");
console.log(deleted);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

deleted = client.conversations.delete("conv_123")
print(deleted)
```
#### Request (csharp)
```csharp
using System;
using OpenAI.Conversations;

OpenAIConversationClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

DeletedConversation deleted = client.DeleteConversation("conv_123");
Console.WriteLine(deleted.Id);
```
#### Response
```json
{
  "id": "conv_123",
  "object": "conversation.deleted",
  "deleted": true
}
```
