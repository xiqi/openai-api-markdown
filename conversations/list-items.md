# List items

Source: https://platform.openai.com/docs/api-reference/conversations/list-items

`GET /v1/conversations/{conversation_id}/items`

List all items for a conversation with the given ID.

## Parameters
- `conversation_id` (path, string, required): The ID of the conversation to list items for.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between
  1 and 100, and the default is 20. Default: `20`.
- `order` (query, string, optional): The order to return the input items in. Default is `desc`.
  - `asc`: Return the input items in ascending order.
  - `desc`: Return the input items in descending order. Enum: 'asc', 'desc'.
- `after` (query, string, optional): An item ID to list items after, used in pagination.
- `include` (query, array<string>, optional): Specify additional output data to include in the model response. Currently supported values are:
  - `web_search_call.action.sources`: Include the sources of the web search tool call.
  - `code_interpreter_call.outputs`: Includes the outputs of python code execution in code interpreter tool call items.
  - `computer_call_output.output.image_url`: Include image urls from the computer call output.
  - `file_search_call.results`: Include the search results of the file search tool call.
  - `message.input_image.image_url`: Include image urls from the input message.
  - `message.output_text.logprobs`: Include logprobs with assistant messages.
  - `reasoning.encrypted_content`: Includes an encrypted version of reasoning tokens in reasoning item outputs. This enables reasoning items to be used in multi-turn conversations when using the Responses API statelessly (like when the `store` parameter is set to `false`, or when an organization is enrolled in the zero data retention program).

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
Returns a [list object](list-items-object.md) containing Conversation items.

## Examples
### List items in a conversation
#### Request (curl)
```bash
curl "https://api.openai.com/v1/conversations/conv_123/items?limit=10" \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const items = await client.conversations.items.list("conv_123", { limit: 10 });
console.log(items.data);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

items = client.conversations.items.list("conv_123", limit=10)
print(items.data)
```
#### Request (csharp)
```csharp
using System;
using OpenAI.Conversations;

OpenAIConversationClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

ConversationItemList items = client.ConversationItems.List(
    conversationId: "conv_123",
    new ListConversationItemsOptions { Limit = 10 }
);
Console.WriteLine(items.Data.Count);
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
    }
  ],
  "first_id": "msg_abc",
  "last_id": "msg_abc",
  "has_more": false
}
```
