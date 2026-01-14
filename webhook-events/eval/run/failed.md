# eval.run.failed

Source: https://platform.openai.com/docs/api-reference/webhook-events/eval/run/failed

Sent when an eval run has failed.

## Properties
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the eval run failed.
- `id` (string, required): The unique ID of the event.
- `data` (object, required): Event data payload.
  - `id` (string, required): The unique ID of the eval run.
- `object` (string, optional): The object of the event. Always `event`. Enum: 'event'.
- `type` (string, required): The type of the event. Always `eval.run.failed`. Enum: 'eval.run.failed'.
