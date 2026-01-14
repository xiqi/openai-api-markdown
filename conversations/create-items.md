# Create items

Source: https://platform.openai.com/docs/api-reference/conversations/create-items

`POST /v1/conversations/{conversation_id}/items`

Create items in a conversation with the given ID.

## Parameters
- `conversation_id` (path, string, required): The ID of the conversation to add the item to.
- `include` (query, array<string>, optional): Additional fields to include in the response. See the `include`
  parameter for [listing Conversation items above](list-items.md#conversations_list_items-include) for more information.

## Request body
### application/json
- `items` (array<object>, required): The items to add to the conversation. You may add up to 20 items at a time.

## Responses
### 200
OK
#### application/json
- `object` (string, required): The type of object returned, must be `list`. Enum: 'list'.
- `data` (array<object>, required): A list of conversation items.
- `has_more` (boolean, required): Whether there are more items available.
- `first_id` (string, required): The ID of the first item in the list.
- `last_id` (string, required): The ID of the last item in the list.

## Returns
Returns the list of added [items](list-items-object.md).

## Examples
### Add a user message to a conversation
#### Request (curl)
```bash
curl https://api.openai.com/v1/conversations/conv_123/items \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "items": [
      {
        "type": "message",
        "role": "user",
        "content": [
          {"type": "input_text", "text": "Hello!"}
        ]
      },
      {
        "type": "message",
        "role": "user",
        "content": [
          {"type": "input_text", "text": "How are you?"}
        ]
      }
    ]
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const items = await client.conversations.items.create(
  "conv_123",
  {
    items: [
      {
        type: "message",
        role: "user",
        content: [{ type: "input_text", text: "Hello!" }],
      },
      {
        type: "message",
        role: "user",
        content: [{ type: "input_text", text: "How are you?" }],
      },
    ],
  }
);
console.log(items.data);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

items = client.conversations.items.create(
  "conv_123",
  items=[
    {
      "type": "message",
      "role": "user",
      "content": [{"type": "input_text", "text": "Hello!"}],
    },
    {
      "type": "message",
      "role": "user",
      "content": [{"type": "input_text", "text": "How are you?"}],
    }
  ],
)
print(items.data)
```
#### Request (csharp)
```csharp
using System;
using System.Collections.Generic;
using OpenAI.Conversations;

OpenAIConversationClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

ConversationItemList created = client.ConversationItems.Create(
    conversationId: "conv_123",
    new CreateConversationItemsOptions
    {
        Items = new List<ConversationItem>
        {
            new ConversationMessage
            {
                Role = "user",
                Content =
                {
                    new ConversationInputText { Text = "Hello!" }
                }
            },
            new ConversationMessage
            {
                Role = "user",
                Content =
                {
                    new ConversationInputText { Text = "How are you?" }
                }
            }
        }
    }
);
Console.WriteLine(created.Data.Count);
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "type": "message",
      "id": "msg_abc",
      "status": "completed",
      "role": "user",
      "content": [
        {"type": "input_text", "text": "Hello!"}
      ]
    },
    {
      "type": "message",
      "id": "msg_def",
      "status": "completed",
      "role": "user",
      "content": [
        {"type": "input_text", "text": "How are you?"}
      ]
    }
  ],
  "first_id": "msg_abc",
  "last_id": "msg_def",
  "has_more": false
}
```
