# conversation.item.input_audio_transcription.failed

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/conversation/item/input_audio_transcription/failed

Returned when input audio transcription is configured, and a transcription 
request for a user message failed. These events are separate from other 
`error` events so that the client can identify the related Item.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be
  `conversation.item.input_audio_transcription.failed`. Enum: 'conversation.item.input_audio_transcription.failed'.
- `item_id` (string, required): The ID of the user message item.
- `content_index` (integer, required): The index of the content part containing the audio.
- `error` (object, required): Details of the transcription error.
  - `type` (string, optional): The type of error.
  - `code` (string, optional): Error code, if any.
  - `message` (string, optional): A human-readable error message.
  - `param` (string, optional): Parameter related to the error, if any.
