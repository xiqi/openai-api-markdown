# Retrieve batch

Source: https://platform.openai.com/docs/api-reference/batch/retrieve

`GET /v1/batches/{batch_id}`

Retrieves a batch.

## Parameters
- `batch_id` (path, string, required): The ID of the batch to retrieve.

## Responses
### 200
Batch retrieved successfully.
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
The [Batch](object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/batches/batch_abc123 \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.batches.retrieve("batch_abc123")
```
#### Response
```json
{
  "id": "batch_abc123",
  "object": "batch",
  "endpoint": "/v1/completions",
  "errors": null,
  "input_file_id": "file-abc123",
  "completion_window": "24h",
  "status": "completed",
  "output_file_id": "file-cvaTdG",
  "error_file_id": "file-HOWS94",
  "created_at": 1711471533,
  "in_progress_at": 1711471538,
  "expires_at": 1711557933,
  "finalizing_at": 1711493133,
  "completed_at": 1711493163,
  "failed_at": null,
  "expired_at": null,
  "cancelling_at": null,
  "cancelled_at": null,
  "request_counts": {
    "total": 100,
    "completed": 95,
    "failed": 5
  },
  "metadata": {
    "customer_id": "user_123456789",
    "batch_description": "Nightly eval job",
  }
}
```
