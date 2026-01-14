# List ChatKit threads

Source: https://platform.openai.com/docs/api-reference/chatkit/threads/list

`GET /v1/chatkit/threads`

List ChatKit threads

## Parameters
- `limit` (query, integer, optional): Maximum number of thread items to return. Defaults to 20.
- `order` (query, string, optional): Sort order for results by creation time. Defaults to `desc`. Enum: 'asc', 'desc'.
- `after` (query, string, optional): List items created after this thread item ID. Defaults to null for the first page.
- `before` (query, string, optional): List items created before this thread item ID. Defaults to null for the newest results.
- `user` (query, string, optional): Filter threads that belong to this user identifier. Defaults to null to return all users.

## Responses
### 200
Success
#### application/json
- `object` (string, required): The type of object returned, must be `list`. Enum: 'list'. Default: `list`.
- `data` (array<object>, required): A list of items
  - Items:
    - `id` (string, required): Identifier of the thread.
    - `object` (string, required): Type discriminator that is always `chatkit.thread`. Enum: 'chatkit.thread'. Default: `chatkit.thread`.
    - `created_at` (integer, required): Unix timestamp (in seconds) for when the thread was created.
    - `title` (string | null, required)
    - `status` (object, required): Current status for the thread. Defaults to `active` for newly created threads.
      - Variant (object):
        - `type` (string, required): Status discriminator that is always `active`. Enum: 'active'. Default: `active`.
      - Variant (object):
        - `type` (string, required): Status discriminator that is always `locked`. Enum: 'locked'. Default: `locked`.
        - `reason` (string | null, required)
      - Variant (object):
        - `type` (string, required): Status discriminator that is always `closed`. Enum: 'closed'. Default: `closed`.
        - `reason` (string | null, required)
    - `user` (string, required): Free-form string that identifies your end user who owns the thread.
- `first_id` (string | null, required)
- `last_id` (string | null, required)
- `has_more` (boolean, required): Whether there are more items available.

## Returns
Returns a paginated list of ChatKit threads accessible to the request scope.

## Examples
### List recent threads
#### Request (curl)
```bash
curl "https://api.openai.com/v1/chatkit/threads?limit=2&order=desc" \
  -H "OpenAI-Beta: chatkit_beta=v1" \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from 'openai';

const client = new OpenAI();

// Automatically fetches more pages as needed.
for await (const chatkitThread of client.beta.chatkit.threads.list()) {
  console.log(chatkitThread.id);
}
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
page = client.beta.chatkit.threads.list()
page = page.data[0]
print(page.id)
```
#### Response
```json
{
  "data": [
    {
      "id": "cthr_abc123",
      "object": "chatkit.thread",
      "title": "Customer escalation"
    },
    {
      "id": "cthr_def456",
      "object": "chatkit.thread",
      "title": "Demo feedback"
    }
  ],
  "has_more": false,
  "object": "list"
}
```
