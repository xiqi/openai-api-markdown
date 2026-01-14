# Cancel upload

Source: https://platform.openai.com/docs/api-reference/uploads/cancel

`POST /v1/uploads/{upload_id}/cancel`

Cancels the Upload. No Parts may be added after an Upload is cancelled.

## Parameters
- `upload_id` (path, string, required): The ID of the Upload.

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
The [Upload](object.md) object with status `cancelled`.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/uploads/upload_abc123/cancel
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
  "status": "cancelled",
  "expires_at": 1719127296
}
```
