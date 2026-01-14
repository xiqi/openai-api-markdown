# Delete a model response

Source: https://platform.openai.com/docs/api-reference/responses/delete

`DELETE /v1/responses/{response_id}`

Deletes a model response with the given ID.

## Parameters
- `response_id` (path, string, required): The ID of the response to delete.

## Responses
### 200
OK
### 404
Not Found
#### application/json
- `code` (string | null, required)
- `message` (string, required)
- `param` (string | null, required)
- `type` (string, required)

## Returns
A success message.

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/responses/resp_123 \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const client = new OpenAI();

const response = await client.responses.delete("resp_123");
console.log(response);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

response = client.responses.delete("resp_123")
print(response)
```
#### Response
```json
{
  "id": "resp_6786a1bec27481909a17d673315b29f6",
  "object": "response",
  "deleted": true
}
```
