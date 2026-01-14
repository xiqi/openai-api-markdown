# Retrieve an item

Source: https://platform.openai.com/docs/api-reference/conversations/get-item

`GET /v1/conversations/{conversation_id}/items/{item_id}`

Get a single item from a conversation with the given IDs.

## Parameters
- `conversation_id` (path, string, required): The ID of the conversation that contains the item.
- `item_id` (path, string, required): The ID of the item to retrieve.
- `include` (query, array<string>, optional): Additional fields to include in the response. See the `include`
  parameter for [listing Conversation items above](list-items.md#conversations_list_items-include) for more information.

## Responses
### 200
OK
#### application/json
- Schema type: `object`

## Returns
Returns a [Conversation Item](https://platform.openai.com/docs/api-reference/conversations/item-object).

## Examples
### Retrieve an item
#### Request (curl)
```bash
curl https://api.openai.com/v1/conversations/conv_123/items/msg_abc \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const item = await client.conversations.items.retrieve(
  "conv_123",
  "msg_abc"
);
console.log(item);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

item = client.conversations.items.retrieve("conv_123", "msg_abc")
print(item)
```
#### Request (csharp)
```csharp
using System;
using OpenAI.Conversations;

OpenAIConversationClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

ConversationItem item = client.ConversationItems.Get(
    conversationId: "conv_123",
    itemId: "msg_abc"
);
Console.WriteLine(item.Id);
```
#### Response
```json
{
  "type": "message",
  "id": "msg_abc",
  "status": "completed",
  "role": "user",
  "content": [
    {"type": "input_text", "text": "Hello!"}
  ]
}
```
