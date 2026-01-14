# response.output_audio.delta

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/response/output_audio/delta

Returned when the model-generated audio is updated.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.output_audio.delta`. Enum: 'response.output_audio.delta'.
- `response_id` (string, required): The ID of the response.
- `item_id` (string, required): The ID of the item.
- `output_index` (integer, required): The index of the output item in the response.
- `content_index` (integer, required): The index of the content part in the item's content array.
- `delta` (string, required): Base64-encoded audio data delta.
