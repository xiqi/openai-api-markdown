# Create batch

Source: https://platform.openai.com/docs/api-reference/batch/create

`POST /v1/batches`

Creates and executes a batch from an uploaded file of requests

## Request body
### application/json
- `input_file_id` (string, required): The ID of an uploaded file that contains requests for the new batch.
  
  See [upload file](../files/create.md) for how to upload a file.
  
  Your input file must be formatted as a [JSONL file](request-input.md), and must be uploaded with the purpose `batch`. The file can contain up to 50,000 requests, and can be up to 200 MB in size.
- `endpoint` (string, required): The endpoint to be used for all requests in the batch. Currently `/v1/responses`, `/v1/chat/completions`, `/v1/embeddings`, `/v1/completions`, and `/v1/moderations` are supported. Note that `/v1/embeddings` batches are also restricted to a maximum of 50,000 embedding inputs across all requests in the batch. Enum: '/v1/responses', '/v1/chat/completions', '/v1/embeddings', '/v1/completions', '/v1/moderations'.
- `completion_window` (string, required): The time frame within which the batch should be processed. Currently only `24h` is supported. Enum: '24h'.
- `metadata` (object | null, optional)
- `output_expires_after` (object, optional): The expiration policy for the output and/or error file that are generated for a batch.
  - `anchor` (string, required): Anchor timestamp after which the expiration policy applies. Supported anchors: `created_at`. Note that the anchor is the file creation time, not the time the batch is created. Enum: 'created_at'.
  - `seconds` (integer, required): The number of seconds after the anchor time that the file will expire. Must be between 3600 (1 hour) and 2592000 (30 days).

## Responses
### 200
Batch created successfully.
#### application/json
- `id` (string, required)
- `object` (string, required): The object type, which is always `batch`. Enum: 'batch'.
- `endpoint` (string, required): The OpenAI API endpoint used by the batch.
- `model` (string, optional): Model ID used to process the batch, like `gpt-5-2025-08-07`. OpenAI
  offers a wide range of models with different capabilities, performance
  characteristics, and price points. Refer to the [model
  guide](https://platform.openai.com/docs/models) to browse and compare available models.
- `errors` (object, optional)
  - `object` (string, optional): The object type, which is always `list`.
  - `data` (array<object>, optional)
    - Items:
      - `code` (string, optional): An error code identifying the error type.
      - `message` (string, optional): A human-readable message providing more details about the error.
      - `param` (string | null, optional)
      - `line` (integer | null, optional)
- `input_file_id` (string, required): The ID of the input file for the batch.
- `completion_window` (string, required): The time frame within which the batch should be processed.
- `status` (string, required): The current status of the batch. Enum: 'validating', 'failed', 'in_progress', 'finalizing', 'completed', 'expired', 'cancelling', 'cancelled'.
- `output_file_id` (string, optional): The ID of the file containing the outputs of successfully executed requests.
- `error_file_id` (string, optional): The ID of the file containing the outputs of requests with errors.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the batch was created.
- `in_progress_at` (integer, optional): The Unix timestamp (in seconds) for when the batch started processing.
- `expires_at` (integer, optional): The Unix timestamp (in seconds) for when the batch will expire.
- `finalizing_at` (integer, optional): The Unix timestamp (in seconds) for when the batch started finalizing.
- `completed_at` (integer, optional): The Unix timestamp (in seconds) for when the batch was completed.
- `failed_at` (integer, optional): The Unix timestamp (in seconds) for when the batch failed.
- `expired_at` (integer, optional): The Unix timestamp (in seconds) for when the batch expired.
- `cancelling_at` (integer, optional): The Unix timestamp (in seconds) for when the batch started cancelling.
- `cancelled_at` (integer, optional): The Unix timestamp (in seconds) for when the batch was cancelled.
- `request_counts` (object, optional): The request counts for different statuses within the batch.
  - `total` (integer, required): Total number of requests in the batch.
  - `completed` (integer, required): Number of requests that have been completed successfully.
  - `failed` (integer, required): Number of requests that have failed.
- `usage` (object, optional): Represents token usage details including input tokens, output tokens, a
  breakdown of output tokens, and the total tokens used. Only populated on
  batches created after September 7, 2025.
  - `input_tokens` (integer, required): The number of input tokens.
  - `input_tokens_details` (object, required): A detailed breakdown of the input tokens.
    - `cached_tokens` (integer, required): The number of tokens that were retrieved from the cache. [More on
      prompt caching](https://platform.openai.com/docs/guides/prompt-caching).
  - `output_tokens` (integer, required): The number of output tokens.
  - `output_tokens_details` (object, required): A detailed breakdown of the output tokens.
    - `reasoning_tokens` (integer, required): The number of reasoning tokens.
  - `total_tokens` (integer, required): The total number of tokens used.
- `metadata` (object | null, optional)

## Returns
The created [Batch](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/batches \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "input_file_id": "file-abc123",
    "endpoint": "/v1/chat/completions",
    "completion_window": "24h"
  }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.batches.create(
  input_file_id="file-abc123",
  endpoint="/v1/chat/completions",
  completion_window="24h"
)
```
#### Response
```json
{
  "id": "batch_abc123",
  "object": "batch",
  "endpoint": "/v1/chat/completions",
  "errors": null,
  "input_file_id": "file-abc123",
  "completion_window": "24h",
  "status": "validating",
  "output_file_id": null,
  "error_file_id": null,
  "created_at": 1711471533,
  "in_progress_at": null,
  "expires_at": null,
  "finalizing_at": null,
  "completed_at": null,
  "failed_at": null,
  "expired_at": null,
  "cancelling_at": null,
  "cancelled_at": null,
  "request_counts": {
    "total": 0,
    "completed": 0,
    "failed": 0
  },
  "metadata": {
    "customer_id": "user_123456789",
    "batch_description": "Nightly eval job",
  }
}
```
