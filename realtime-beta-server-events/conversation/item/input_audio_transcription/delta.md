# conversation.item.input_audio_transcription.delta

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/conversation/item/input_audio_transcription/delta

Returned when the text value of an input audio transcription content part is updated.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `conversation.item.input_audio_transcription.delta`. Enum: 'conversation.item.input_audio_transcription.delta'.
- `item_id` (string, required): The ID of the item.
- `content_index` (integer, optional): The index of the content part in the item's content array.
- `delta` (string, optional): The text delta.
- `logprobs` (array<object> | null, optional)
