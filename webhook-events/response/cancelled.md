# response.cancelled

Source: https://platform.openai.com/docs/api-reference/webhook-events/response/cancelled

Sent when a background response has been cancelled.

## Properties
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the model response was cancelled.
- `id` (string, required): The unique ID of the event.
- `data` (object, required): Event data payload.
  - `id` (string, required): The unique ID of the model response.
- `object` (string, optional): The object of the event. Always `event`. Enum: 'event'.
- `type` (string, required): The type of the event. Always `response.cancelled`. Enum: 'response.cancelled'.
