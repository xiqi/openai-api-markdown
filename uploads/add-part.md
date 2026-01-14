# Add upload part

Source: https://platform.openai.com/docs/api-reference/uploads/add-part

`POST /v1/uploads/{upload_id}/parts`

Adds a [Part](part-object.md) to an [Upload](object.md) object. A Part represents a chunk of bytes from the file you are trying to upload. 

Each Part can be at most 64 MB, and you can add Parts until you hit the Upload maximum of 8 GB.

It is possible to add multiple Parts in parallel. You can decide the intended order of the Parts when you [complete the Upload](complete.md).

## Parameters
- `upload_id` (path, string, required): The ID of the Upload.

## Request body
### multipart/form-data
- `data` (string, required): The chunk of bytes for this Part.

## Responses
### 200
OK
#### application/json
- `id` (string, required): The upload Part unique identifier, which can be referenced in API endpoints.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the Part was created.
- `upload_id` (string, required): The ID of the Upload object that this Part was added to.
- `object` (string, required): The object type, which is always `upload.part`. Enum: 'upload.part'.

## Returns
The upload [Part](part-object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/uploads/upload_abc123/parts
  -F data="aHR0cHM6Ly9hcGkub3BlbmFpLmNvbS92MS91cGxvYWRz..."
```
#### Response
```json
{
  "id": "part_def456",
  "object": "upload.part",
  "created_at": 1719185911,
  "upload_id": "upload_abc123"
}
```
