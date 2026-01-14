# input_audio_buffer.clear

Source: https://platform.openai.com/docs/api-reference/realtime-client-events/input_audio_buffer/clear

Send this event to clear the audio bytes in the buffer. The server will 
respond with an `input_audio_buffer.cleared` event.

## Properties
- `event_id` (string, optional): Optional client-generated ID used to identify this event.
- `type` (string, required): The event type, must be `input_audio_buffer.clear`. Enum: 'input_audio_buffer.clear'.
