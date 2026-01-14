# input_audio_buffer.committed

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/input_audio_buffer/committed

Returned when an input audio buffer is committed, either by the client or
automatically in server VAD mode. The `item_id` property is the ID of the user
message item that will be created, thus a `conversation.item.created` event
will also be sent to the client.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `input_audio_buffer.committed`. Enum: 'input_audio_buffer.committed'.
- `previous_item_id` (string | null, optional)
- `item_id` (string, required): The ID of the user message item that will be created.
