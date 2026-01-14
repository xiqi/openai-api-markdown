# List files

Source: https://platform.openai.com/docs/api-reference/files/list

`GET /v1/files`

Returns a list of files.

## Parameters
- `purpose` (query, string, optional): Only return files with the given purpose.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 10,000, and the default is 10,000. Default: `10000`.
- `order` (query, string, optional): Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and `desc` for descending order. Enum: 'asc', 'desc'. Default: `desc`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.

## Responses
### 200
OK
#### application/json
- `object` (string, required)
- `data` (array<object>, required)
  - Items:
    - `id` (string, required): The file identifier, which can be referenced in the API endpoints.
    - `bytes` (integer, required): The size of the file, in bytes.
    - `created_at` (integer, required): The Unix timestamp (in seconds) for when the file was created.
    - `expires_at` (integer, optional): The Unix timestamp (in seconds) for when the file will expire.
    - `filename` (string, required): The name of the file.
    - `object` (string, required): The object type, which is always `file`. Enum: 'file'.
    - `purpose` (string, required): The intended purpose of the file. Supported values are `assistants`, `assistants_output`, `batch`, `batch_output`, `fine-tune`, `fine-tune-results`, `vision`, and `user_data`. Enum: 'assistants', 'assistants_output', 'batch', 'batch_output', 'fine-tune', 'fine-tune-results', 'vision', 'user_data'.
    - `status` (string, required): Deprecated. The current status of the file, which can be either `uploaded`, `processed`, or `error`. Enum: 'uploaded', 'processed', 'error'. Deprecated.
    - `status_details` (string, optional): Deprecated. For details on why a fine-tuning training file failed validation, see the `error` field on `fine_tuning.job`. Deprecated.
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [File](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/files \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.files.list()
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "id": "file-abc123",
      "object": "file",
      "bytes": 175,
      "created_at": 1613677385,
      "expires_at": 1677614202,
      "filename": "salesOverview.pdf",
      "purpose": "assistants",
    },
    {
      "id": "file-abc456",
      "object": "file",
      "bytes": 140,
      "created_at": 1613779121,
      "expires_at": 1677614202,
      "filename": "puppy.jsonl",
      "purpose": "fine-tune",
    }
  ],
  "first_id": "file-abc123",
  "last_id": "file-abc456",
  "has_more": false
}
```
