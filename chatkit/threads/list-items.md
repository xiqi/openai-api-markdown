# List ChatKit thread items

Source: https://platform.openai.com/docs/api-reference/chatkit/threads/list-items

`GET /v1/chatkit/threads/{thread_id}/items`

List ChatKit thread items

## Parameters
- `thread_id` (path, string, required): Identifier of the ChatKit thread whose items are requested.
- `limit` (query, integer, optional): Maximum number of thread items to return. Defaults to 20.
- `order` (query, string, optional): Sort order for results by creation time. Defaults to `desc`. Enum: 'asc', 'desc'.
- `after` (query, string, optional): List items created after this thread item ID. Defaults to null for the first page.
- `before` (query, string, optional): List items created before this thread item ID. Defaults to null for the newest results.

## Responses
### 200
Success
#### application/json
- `object` (string, required): The type of object returned, must be `list`. Enum: 'list'. Default: `list`.
- `data` (array<object>, required): A list of items
- `first_id` (string | null, required)
- `last_id` (string | null, required)
- `has_more` (boolean, required): Whether there are more items available.

## Returns
Returns a [list of thread items](item-list.md) for the specified thread.

## Examples
### Retrieve items for a thread
#### Request (curl)
```bash
curl "https://api.openai.com/v1/chatkit/threads/cthr_abc123/items?limit=3" \
  -H "OpenAI-Beta: chatkit_beta=v1" \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from 'openai';

const client = new OpenAI();

// Automatically fetches more pages as needed.
for await (const thread of client.beta.chatkit.threads.listItems('cthr_123')) {
  console.log(thread);
}
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
page = client.beta.chatkit.threads.list_items(
    thread_id="cthr_123",
)
page = page.data[0]
print(page)
```
#### Response
```json
{
  "data": [
    {
      "id": "cthi_user_001",
      "object": "chatkit.thread_item",
      "type": "user_message",
      "content": [
        {
          "type": "input_text",
          "text": "I need help debugging an onboarding issue."
        }
      ],
      "attachments": []
    },
    {
      "id": "cthi_assistant_002",
      "object": "chatkit.thread_item",
      "type": "assistant_message",
      "content": [
        {
          "type": "output_text",
          "text": "Let's start by confirming the workflow version you deployed."
        }
      ]
    }
  ],
  "has_more": false,
  "object": "list"
}
```
