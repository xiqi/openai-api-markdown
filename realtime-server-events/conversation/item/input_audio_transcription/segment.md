# conversation.item.input_audio_transcription.segment

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/conversation/item/input_audio_transcription/segment

Returned when an input audio transcription segment is identified for an item.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `conversation.item.input_audio_transcription.segment`. Enum: 'conversation.item.input_audio_transcription.segment'.
- `item_id` (string, required): The ID of the item containing the input audio content.
- `content_index` (integer, required): The index of the input audio content part within the item.
- `text` (string, required): The text for this segment.
- `id` (string, required): The segment identifier.
- `speaker` (string, required): The detected speaker label for this segment.
- `start` (number, required): Start time of the segment in seconds.
- `end` (number, required): End time of the segment in seconds.
