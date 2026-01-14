# Retrieve container file

Source: https://platform.openai.com/docs/api-reference/container-files/retrieveContainerFile

`GET /v1/containers/{container_id}/files/{file_id}`

Retrieve Container File

## Parameters
- `container_id` (path, string, required)
- `file_id` (path, string, required)

## Responses
### 200
Success
#### application/json
- `id` (string, required): Unique identifier for the file.
- `object` (string, required): The type of this object (`container.file`).
- `container_id` (string, required): The container this file belongs to.
- `created_at` (integer, required): Unix timestamp (in seconds) when the file was created.
- `bytes` (integer, required): Size of the file in bytes.
- `path` (string, required): Path of the file in the container.
- `source` (string, required): Source of the file (e.g., `user`, `assistant`).

## Returns
The [container file](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/containers/container_123/files/file_456 \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
{
    "id": "cfile_682e0e8a43c88191a7978f477a09bdf5",
    "object": "container.file",
    "created_at": 1747848842,
    "bytes": 880,
    "container_id": "cntr_682e0e7318108198aa783fd921ff305e08e78805b9fdbb04",
    "path": "/mnt/data/88e12fa445d32636f190a0b33daed6cb-tsconfig.json",
    "source": "user"
}
```
