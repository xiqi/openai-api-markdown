# fine_tuning.job.succeeded

Source: https://platform.openai.com/docs/api-reference/webhook-events/fine_tuning/job/succeeded

Sent when a fine-tuning job has succeeded.

## Properties
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the fine-tuning job succeeded.
- `id` (string, required): The unique ID of the event.
- `data` (object, required): Event data payload.
  - `id` (string, required): The unique ID of the fine-tuning job.
- `object` (string, optional): The object of the event. Always `event`. Enum: 'event'.
- `type` (string, required): The type of the event. Always `fine_tuning.job.succeeded`. Enum: 'fine_tuning.job.succeeded'.
