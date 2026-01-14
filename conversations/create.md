# Create a conversation

Source: https://platform.openai.com/docs/api-reference/conversations/create

`POST /v1/conversations`

Create a conversation.

## Request body
### application/json
- `metadata` (object | null | null, optional)
- `items` (array<object> | null, optional)

## Responses
### 200
Success
#### application/json
- `id` (string, required): The unique ID of the conversation.
- `object` (string, required): The object type, which is always `conversation`. Enum: 'conversation'. Default: `conversation`.
- `metadata` (object, required): Set of 16 key-value pairs that can be attached to an object. This can be         useful for storing additional information about the object in a structured         format, and querying for objects via API or the dashboard.
          Keys are strings with a maximum length of 64 characters. Values are strings         with a maximum length of 512 characters.
- `created_at` (integer, required): The time at which the conversation was created, measured in seconds since the Unix epoch.

## Returns
Returns a [Conversation](object.md) object.

## Examples
### Create a conversation.
#### Request (curl)
```bash
curl https://api.openai.com/v1/conversations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "metadata": {"topic": "demo"},
    "items": [
      {
        "type": "message",
        "role": "user",
        "content": "Hello!"
      }
    ]
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const conversation = await client.conversations.create({
  metadata: { topic: "demo" },
  items: [
    { type: "message", role: "user", content: "Hello!" }
  ],
});
console.log(conversation);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

conversation = client.conversations.create(
  metadata={"topic": "demo"},
  items=[
    {"type": "message", "role": "user", "content": "Hello!"}
  ]
)
print(conversation)
```
#### Request (csharp)
```csharp
using System;
using System.Collections.Generic;
using OpenAI.Conversations;

OpenAIConversationClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

Conversation conversation = client.CreateConversation(
    new CreateConversationOptions
    {
        Metadata = new Dictionary<string, string>
        {
            { "topic", "demo" }
        },
        Items =
        {
            new ConversationMessageInput
            {
                Role = "user",
                Content = "Hello!",
            }
        }
    }
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
