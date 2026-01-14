# fine_tuning.job.failed

Source: https://platform.openai.com/docs/api-reference/webhook-events/fine_tuning/job/failed

Sent when a fine-tuning job has failed.

## Properties
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the fine-tuning job failed.
- `id` (string, required): The unique ID of the event.
- `data` (object, required): Event data payload.
  - `id` (string, required): The unique ID of the fine-tuning job.
- `object` (string, optional): The object of the event. Always `event`. Enum: 'event'.
- `type` (string, required): The type of the event. Always `fine_tuning.job.failed`. Enum: 'fine_tuning.job.failed'.
