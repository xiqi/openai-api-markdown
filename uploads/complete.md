# Complete upload

Source: https://platform.openai.com/docs/api-reference/uploads/complete

`POST /v1/uploads/{upload_id}/complete`

Completes the [Upload](object.md). 

Within the returned Upload object, there is a nested [File](../files/object.md) object that is ready to use in the rest of the platform.

You can specify the order of the Parts by passing in an ordered list of the Part IDs.

The number of bytes uploaded upon completion must match the number of bytes initially specified when creating the Upload object. No Parts may be added after an Upload is completed.

## Parameters
- `upload_id` (path, string, required): The ID of the Upload.

## Request body
### application/json
- `part_ids` (array<string>, required): The ordered list of Part IDs.
- `md5` (string, optional): The optional md5 checksum for the file contents to verify if the bytes uploaded matches what you expect.

## Responses
### 200
OK
#### application/json
- `id` (string, required): The Upload unique identifier, which can be referenced in API endpoints.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the Upload was created.
- `filename` (string, required): The name of the file to be uploaded.
- `bytes` (integer, required): The intended number of bytes to be uploaded.
- `purpose` (string, required): The intended purpose of the file. [Please refer here](../files/object.md#files/object-purpose) for acceptable values.
- `status` (string, required): The status of the Upload. Enum: 'pending', 'completed', 'cancelled', 'expired'.
- `expires_at` (integer, required): The Unix timestamp (in seconds) for when the Upload will expire.
- `object` (string, optional): The object type, which is always "upload". Enum: 'upload'.
- `file` (object, optional): The ready File object after the Upload is completed.
  - `id` (string, required): The file identifier, which can be referenced in the API endpoints.
  - `bytes` (integer, required): The size of the file, in bytes.
  - `created_at` (integer, required): The Unix timestamp (in seconds) for when the file was created.
  - `expires_at` (integer, optional): The Unix timestamp (in seconds) for when the file will expire.
  - `filename` (string, required): The name of the file.
  - `object` (string, required): The object type, which is always `file`. Enum: 'file'.
  - `purpose` (string, required): The intended purpose of the file. Supported values are `assistants`, `assistants_output`, `batch`, `batch_output`, `fine-tune`, `fine-tune-results`, `vision`, and `user_data`. Enum: 'assistants', 'assistants_output', 'batch', 'batch_output', 'fine-tune', 'fine-tune-results', 'vision', 'user_data'.
  - `status` (string, required): Deprecated. The current status of the file, which can be either `uploaded`, `processed`, or `error`. Enum: 'uploaded', 'processed', 'error'. Deprecated.
  - `status_details` (string, optional): Deprecated. For details on why a fine-tuning training file failed validation, see the `error` field on `fine_tuning.job`. Deprecated.

## Returns
The [Upload](object.md) object with status `completed` with an additional `file` property containing the created usable File object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/uploads/upload_abc123/complete
  -d '{
    "part_ids": ["part_def456", "part_ghi789"]
  }'
```
#### Response
```json
{
  "id": "upload_abc123",
  "object": "upload",
  "bytes": 2147483648,
  "created_at": 1719184911,
  "filename": "training_examples.jsonl",
  "purpose": "fine-tune",
  "status": "completed",
  "expires_at": 1719127296,
  "file": {
    "id": "file-xyz321",
    "object": "file",
    "bytes": 2147483648,
    "created_at": 1719186911,
    "expires_at": 1719127296,
    "filename": "training_examples.jsonl",
    "purpose": "fine-tune",
  }
}
```
