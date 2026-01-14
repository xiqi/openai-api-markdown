# response.incomplete

Source: https://platform.openai.com/docs/api-reference/webhook-events/response/incomplete

Sent when a background response has been interrupted.

## Properties
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the model response was interrupted.
- `id` (string, required): The unique ID of the event.
- `data` (object, required): Event data payload.
  - `id` (string, required): The unique ID of the model response.
- `object` (string, optional): The object of the event. Always `event`. Enum: 'event'.
- `type` (string, required): The type of the event. Always `response.incomplete`. Enum: 'response.incomplete'.
