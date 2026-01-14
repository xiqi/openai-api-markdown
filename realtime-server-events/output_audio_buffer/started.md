# output_audio_buffer.started

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/output_audio_buffer/started

**WebRTC/SIP Only:** Emitted when the server begins streaming audio to the client. This event is
emitted after an audio content part has been added (`response.content_part.added`)
to the response.
[Learn more](https://platform.openai.com/docs/guides/realtime-conversations#client-and-server-events-for-audio-in-webrtc).

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `output_audio_buffer.started`. Enum: 'output_audio_buffer.started'.
- `response_id` (string, required): The unique ID of the response that produced the audio.
