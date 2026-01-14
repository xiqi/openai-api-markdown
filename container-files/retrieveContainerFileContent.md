# Retrieve container file content

Source: https://platform.openai.com/docs/api-reference/container-files/retrieveContainerFileContent

`GET /v1/containers/{container_id}/files/{file_id}/content`

Retrieve Container File Content

## Parameters
- `container_id` (path, string, required)
- `file_id` (path, string, required)

## Responses
### 200
Success

## Returns
The contents of the container file.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/containers/container_123/files/cfile_456/content \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
<binary content of the file>
```
