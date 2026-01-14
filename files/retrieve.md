# Retrieve file

Source: https://platform.openai.com/docs/api-reference/files/retrieve

`GET /v1/files/{file_id}`

Returns information about a specific file.

## Parameters
- `file_id` (path, string, required): The ID of the file to use for this request.

## Responses
### 200
OK
#### application/json
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
The [File](object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/files/file-abc123 \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.files.retrieve("file-abc123")
```
#### Response
```json
{
  "id": "file-abc123",
  "object": "file",
  "bytes": 120000,
  "created_at": 1677610602,
  "expires_at": 1677614202,
  "filename": "mydata.jsonl",
  "purpose": "fine-tune",
}
```
