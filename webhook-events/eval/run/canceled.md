# eval.run.canceled

Source: https://platform.openai.com/docs/api-reference/webhook-events/eval/run/canceled

Sent when an eval run has been canceled.

## Properties
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the eval run was canceled.
- `id` (string, required): The unique ID of the event.
- `data` (object, required): Event data payload.
  - `id` (string, required): The unique ID of the eval run.
- `object` (string, optional): The object of the event. Always `event`. Enum: 'event'.
- `type` (string, required): The type of the event. Always `eval.run.canceled`. Enum: 'eval.run.canceled'.
