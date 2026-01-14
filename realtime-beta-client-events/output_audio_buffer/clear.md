# output_audio_buffer.clear

Source: https://platform.openai.com/docs/api-reference/realtime-beta-client-events/output_audio_buffer/clear

**WebRTC/SIP Only:** Emit to cut off the current audio response. This will trigger the server to
stop generating audio and emit a `output_audio_buffer.cleared` event. This
event should be preceded by a `response.cancel` client event to stop the
generation of the current response.
[Learn more](https://platform.openai.com/docs/guides/realtime-conversations#client-and-server-events-for-audio-in-webrtc).

## Properties
- `event_id` (string, optional): The unique ID of the client event used for error handling.
- `type` (string, required): The event type, must be `output_audio_buffer.clear`. Enum: 'output_audio_buffer.clear'.
