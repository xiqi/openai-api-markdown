# input_audio_buffer.cleared

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/input_audio_buffer/cleared

Returned when the input audio buffer is cleared by the client with a 
`input_audio_buffer.clear` event.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `input_audio_buffer.cleared`. Enum: 'input_audio_buffer.cleared'.
