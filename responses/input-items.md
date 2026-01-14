# List input items

Source: https://platform.openai.com/docs/api-reference/responses/input-items

`GET /v1/responses/{response_id}/input_items`

Returns a list of input items for a given response.

## Parameters
- `response_id` (path, string, required): The ID of the response to retrieve input items for.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between
  1 and 100, and the default is 20. Default: `20`.
- `order` (query, string, optional): The order to return the input items in. Default is `desc`.
  - `asc`: Return the input items in ascending order.
  - `desc`: Return the input items in descending order. Enum: 'asc', 'desc'.
- `after` (query, string, optional): An item ID to list items after, used in pagination.
- `include` (query, array<string>, optional): Additional fields to include in the response. See the `include`
  parameter for Response creation above for more information.

## Responses
### 200
OK
#### application/json
- `object` (string, required): The type of object returned, must be `list`. Enum: 'list'.
- `data` (array<object>, required): A list of items used to generate this response.
- `has_more` (boolean, required): Whether there are more items available.
- `first_id` (string, required): The ID of the first item in the list.
- `last_id` (string, required): The ID of the last item in the list.

## Returns
A list of input item objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/responses/resp_abc123/input_items \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.inputItems.list("resp_123");
console.log(response.data);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

response = client.responses.input_items.list("resp_123")
print(response.data)
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "id": "msg_abc123",
      "type": "message",
      "role": "user",
      "content": [
        {
          "type": "input_text",
          "text": "Tell me a three sentence bedtime story about a unicorn."
        }
      ]
    }
  ],
  "first_id": "msg_abc123",
  "last_id": "msg_abc123",
  "has_more": false
}
```
