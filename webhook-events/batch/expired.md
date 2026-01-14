# batch.expired

Source: https://platform.openai.com/docs/api-reference/webhook-events/batch/expired

Sent when a batch API request has expired.

## Properties
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the batch API request expired.
- `id` (string, required): The unique ID of the event.
- `data` (object, required): Event data payload.
  - `id` (string, required): The unique ID of the batch API request.
- `object` (string, optional): The object of the event. Always `event`. Enum: 'event'.
- `type` (string, required): The type of the event. Always `batch.expired`. Enum: 'batch.expired'.
