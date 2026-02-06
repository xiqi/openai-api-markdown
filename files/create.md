# Upload file

Source: https://platform.openai.com/docs/api-reference/files/create

`POST /v1/files`

Upload a file that can be used across various endpoints. Individual files
can be up to 512 MB, and each project can store up to 2.5 TB of files in
total. There is no organization-wide storage limit.

- The Assistants API supports files up to 2 million tokens and of specific
  file types. See the [Assistants Tools guide](https://platform.openai.com/docs/assistants/tools) for
  details.
- The Fine-tuning API only supports `.jsonl` files. The input also has
  certain required formats for fine-tuning
  [chat](../fine-tuning/chat-input.md) or
  [completions](https://platform.openai.com/docs/api-reference/fine-tuning/completions-input) models.
- The Batch API only supports `.jsonl` files up to 200 MB in size. The input
  also has a specific required
  [format](../batch/request-input.md).

Please [contact us](https://help.openai.com/) if you need to increase these
storage limits.

## Request body
### multipart/form-data
- `file` (string, required): The File object (not file name) to be uploaded.
- `purpose` (string, required): The intended purpose of the uploaded file. One of:
  - `assistants`: Used in the Assistants API
  - `batch`: Used in the Batch API
  - `fine-tune`: Used for fine-tuning
  - `vision`: Images used for vision fine-tuning
  - `user_data`: Flexible file type for any purpose
  - `evals`: Used for eval data sets Enum: 'assistants', 'batch', 'fine-tune', 'vision', 'user_data', 'evals'.
- `expires_after` (object, optional): The expiration policy for a file. By default, files with `purpose=batch` expire after 30 days and all other files are persisted until they are manually deleted.
  - `anchor` (string, required): Anchor timestamp after which the expiration policy applies. Supported anchors: `created_at`. Enum: 'created_at'.
  - `seconds` (integer, required): The number of seconds after the anchor time that the file will expire. Must be between 3600 (1 hour) and 2592000 (30 days).

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
The uploaded [File](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/files \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F purpose="fine-tune" \
  -F file="@mydata.jsonl"
  -F expires_after[anchor]="created_at"
  -F expires_after[seconds]=2592000
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.files.create(
  file=open("mydata.jsonl", "rb"),
  purpose="fine-tune",
  expires_after={
    "anchor": "created_at",
    "seconds": 2592000
  }
)
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
