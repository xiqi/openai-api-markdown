# Delete a container file

Source: https://platform.openai.com/docs/api-reference/container-files/deleteContainerFile

`DELETE /v1/containers/{container_id}/files/{file_id}`

Delete Container File

## Parameters
- `container_id` (path, string, required)
- `file_id` (path, string, required)

## Responses
### 200
OK

## Returns
Deletion Status

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/containers/cntr_682dfebaacac8198bbfe9c2474fb6f4a085685cbe3cb5863/files/cfile_682e0e8a43c88191a7978f477a09bdf5 \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
{
    "id": "cfile_682e0e8a43c88191a7978f477a09bdf5",
    "object": "container.file.deleted",
    "deleted": true
}
```
