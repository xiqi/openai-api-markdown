# response.content_part.added

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/response/content_part/added

Returned when a new content part is added to an assistant message item during
response generation.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.content_part.added`. Enum: 'response.content_part.added'.
- `response_id` (string, required): The ID of the response.
- `item_id` (string, required): The ID of the item to which the content part was added.
- `output_index` (integer, required): The index of the output item in the response.
- `content_index` (integer, required): The index of the content part in the item's content array.
- `part` (object, required): The content part that was added.
  - `type` (string, optional): The content type ("text", "audio"). Enum: 'audio', 'text'.
  - `text` (string, optional): The text content (if type is "text").
  - `audio` (string, optional): Base64-encoded audio data (if type is "audio").
  - `transcript` (string, optional): The transcript of the audio (if type is "audio").
