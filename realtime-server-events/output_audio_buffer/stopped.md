# output_audio_buffer.stopped

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/output_audio_buffer/stopped

**WebRTC/SIP Only:** Emitted when the output audio buffer has been completely drained on the server,
and no more audio is forthcoming. This event is emitted after the full response
data has been sent to the client (`response.done`).
[Learn more](https://platform.openai.com/docs/guides/realtime-conversations#client-and-server-events-for-audio-in-webrtc).

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `output_audio_buffer.stopped`. Enum: 'output_audio_buffer.stopped'.
- `response_id` (string, required): The unique ID of the response that produced the audio.
