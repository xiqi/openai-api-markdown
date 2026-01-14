# Delete file

Source: https://platform.openai.com/docs/api-reference/files/delete

`DELETE /v1/files/{file_id}`

Delete a file and remove it from all vector stores.

## Parameters
- `file_id` (path, string, required): The ID of the file to use for this request.

## Responses
### 200
OK
#### application/json
- `id` (string, required)
- `object` (string, required) Enum: 'file'.
- `deleted` (boolean, required)

## Returns
Deletion status.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/files/file-abc123 \
  -X DELETE \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.files.delete("file-abc123")
```
#### Response
```json
{
  "id": "file-abc123",
  "object": "file",
  "deleted": true
}
```
