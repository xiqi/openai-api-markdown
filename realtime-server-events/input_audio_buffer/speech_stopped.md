# input_audio_buffer.speech_stopped

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/input_audio_buffer/speech_stopped

Returned in `server_vad` mode when the server detects the end of speech in 
the audio buffer. The server will also send an `conversation.item.created` 
event with the user message item that is created from the audio buffer.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `input_audio_buffer.speech_stopped`. Enum: 'input_audio_buffer.speech_stopped'.
- `audio_end_ms` (integer, required): Milliseconds since the session started when speech stopped. This will 
  correspond to the end of audio sent to the model, and thus includes the 
  `min_silence_duration_ms` configured in the Session.
- `item_id` (string, required): The ID of the user message item that will be created.
