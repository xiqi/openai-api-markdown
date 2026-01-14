# conversation.item.truncated

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/conversation/item/truncated

Returned when an earlier assistant audio message item is truncated by the 
client with a `conversation.item.truncate` event. This event is used to 
synchronize the server's understanding of the audio with the client's playback.

This action will truncate the audio and remove the server-side text transcript 
to ensure there is no text in the context that hasn't been heard by the user.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `conversation.item.truncated`. Enum: 'conversation.item.truncated'.
- `item_id` (string, required): The ID of the assistant message item that was truncated.
- `content_index` (integer, required): The index of the content part that was truncated.
- `audio_end_ms` (integer, required): The duration up to which the audio was truncated, in milliseconds.
