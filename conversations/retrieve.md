# Retrieve a conversation

Source: https://platform.openai.com/docs/api-reference/conversations/retrieve

`GET /v1/conversations/{conversation_id}`

Get a conversation

## Parameters
- `conversation_id` (path, string, required): The ID of the conversation to retrieve.

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
### Retrieve a conversation
#### Request (curl)
```bash
curl https://api.openai.com/v1/conversations/conv_123 \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const conversation = await client.conversations.retrieve("conv_123");
console.log(conversation);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

conversation = client.conversations.retrieve("conv_123")
print(conversation)
```
#### Request (csharp)
```csharp
using System;
using OpenAI.Conversations;

OpenAIConversationClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

Conversation conversation = client.GetConversation("conv_123");
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
