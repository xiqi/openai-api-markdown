# Update a conversation

Source: https://platform.openai.com/docs/api-reference/conversations/update

`POST /v1/conversations/{conversation_id}`

Update a conversation

## Parameters
- `conversation_id` (path, string, required): The ID of the conversation to update.

## Request body
### application/json
- `metadata` (object | null, required): Set of 16 key-value pairs that can be attached to an object. This can be         useful for storing additional information about the object in a structured         format, and querying for objects via API or the dashboard.
          Keys are strings with a maximum length of 64 characters. Values are strings         with a maximum length of 512 characters.

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
Returns the updated [Conversation](object.md) object.

## Examples
### Update conversation metadata
#### Request (curl)
```bash
curl https://api.openai.com/v1/conversations/conv_123 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "metadata": {"topic": "project-x"}
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const updated = await client.conversations.update(
  "conv_123",
  { metadata: { topic: "project-x" } }
);
console.log(updated);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

updated = client.conversations.update(
  "conv_123",
  metadata={"topic": "project-x"}
)
print(updated)
```
#### Request (csharp)
```csharp
using System;
using System.Collections.Generic;
using OpenAI.Conversations;

OpenAIConversationClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

Conversation updated = client.UpdateConversation(
    conversationId: "conv_123",
    new UpdateConversationOptions
    {
        Metadata = new Dictionary<string, string>
        {
            { "topic", "project-x" }
        }
    }
);
Console.WriteLine(updated.Id);
```
#### Response
```json
{
  "id": "conv_123",
  "object": "conversation",
  "created_at": 1741900000,
  "metadata": {"topic": "project-x"}
}
```
