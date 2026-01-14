# Delete an item

Source: https://platform.openai.com/docs/api-reference/conversations/delete-item

`DELETE /v1/conversations/{conversation_id}/items/{item_id}`

Delete an item from a conversation with the given IDs.

## Parameters
- `conversation_id` (path, string, required): The ID of the conversation that contains the item.
- `item_id` (path, string, required): The ID of the item to delete.

## Responses
### 200
OK
#### application/json
- `id` (string, required): The unique ID of the conversation.
- `object` (string, required): The object type, which is always `conversation`. Enum: 'conversation'. Default: `conversation`.
- `metadata` (object, required): Set of 16 key-value pairs that can be attached to an object. This can be         useful for storing additional information about the object in a structured         format, and querying for objects via API or the dashboard.
          Keys are strings with a maximum length of 64 characters. Values are strings         with a maximum length of 512 characters.
- `created_at` (integer, required): The time at which the conversation was created, measured in seconds since the Unix epoch.

## Returns
Returns the updated [Conversation](object.md) object.

## Examples
### Delete an item
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/conversations/conv_123/items/msg_abc \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const conversation = await client.conversations.items.delete(
  "conv_123",
  "msg_abc"
);
console.log(conversation);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

conversation = client.conversations.items.delete("conv_123", "msg_abc")
print(conversation)
```
#### Request (csharp)
```csharp
using System;
using OpenAI.Conversations;

OpenAIConversationClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

Conversation conversation = client.ConversationItems.Delete(
    conversationId: "conv_123",
    itemId: "msg_abc"
);
Console.WriteLine(conversation.Id);
```
#### Response
```json
{
  "id": "conv_123",
  "object": "conversation",
  "created_at": 1741900000,
  "metadata": {"topic": "demo"}
}
```
