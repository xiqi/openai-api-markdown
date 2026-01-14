# Create upload

Source: https://platform.openai.com/docs/api-reference/uploads/create

`POST /v1/uploads`

Creates an intermediate [Upload](object.md) object
that you can add [Parts](part-object.md) to.
Currently, an Upload can accept at most 8 GB in total and expires after an
hour after you create it.

Once you complete the Upload, we will create a
[File](../files/object.md) object that contains all the parts
you uploaded. This File is usable in the rest of our platform as a regular
File object.

For certain `purpose` values, the correct `mime_type` must be specified. 
Please refer to documentation for the 
[supported MIME types for your use case](https://platform.openai.com/docs/assistants/tools/file-search#supported-files).

For guidance on the proper filename extensions for each purpose, please
follow the documentation on [creating a
File](../files/create.md).

## Request body
### application/json
- `filename` (string, required): The name of the file to upload.
- `purpose` (string, required): The intended purpose of the uploaded file.
  
  See the [documentation on File purposes](../files/create.md#files-create-purpose). Enum: 'assistants', 'batch', 'fine-tune', 'vision'.
- `bytes` (integer, required): The number of bytes in the file you are uploading.
- `mime_type` (string, required): The MIME type of the file.
  
  This must fall within the supported MIME types for your file purpose. See the supported MIME types for assistants and vision.
- `expires_after` (object, optional): The expiration policy for a file. By default, files with `purpose=batch` expire after 30 days and all other files are persisted until they are manually deleted.
  - `anchor` (string, required): Anchor timestamp after which the expiration policy applies. Supported anchors: `created_at`. Enum: 'created_at'.
  - `seconds` (integer, required): The number of seconds after the anchor time that the file will expire. Must be between 3600 (1 hour) and 2592000 (30 days).

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
The [Upload](object.md) object with status `pending`.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/uploads \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "purpose": "fine-tune",
    "filename": "training_examples.jsonl",
    "bytes": 2147483648,
    "mime_type": "text/jsonl",
    "expires_after": {
      "anchor": "created_at",
      "seconds": 3600
    }
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
  "status": "pending",
  "expires_at": 1719127296
}
```
