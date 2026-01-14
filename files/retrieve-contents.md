# Retrieve file content

Source: https://platform.openai.com/docs/api-reference/files/retrieve-contents

`GET /v1/files/{file_id}/content`

Returns the contents of the specified file.

## Parameters
- `file_id` (path, string, required): The ID of the file to use for this request.

## Responses
### 200
OK
#### application/json
- Schema type: `string`

## Returns
The file content.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/files/file-abc123/content \
  -H "Authorization: Bearer $OPENAI_API_KEY" > file.jsonl
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

content = client.files.content("file-abc123")
```
