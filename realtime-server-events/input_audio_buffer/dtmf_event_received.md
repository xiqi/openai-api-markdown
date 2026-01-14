# input_audio_buffer.dtmf_event_received

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/input_audio_buffer/dtmf_event_received

**SIP Only:** Returned when an DTMF event is received. A DTMF event is a message that
represents a telephone keypad press (0–9, *, #, A–D). The `event` property
is the keypad that the user press. The `received_at` is the UTC Unix Timestamp
that the server received the event.

## Properties
- `type` (string, required): The event type, must be `input_audio_buffer.dtmf_event_received`. Enum: 'input_audio_buffer.dtmf_event_received'.
- `event` (string, required): The telephone keypad that was pressed by the user.
- `received_at` (integer, required): UTC Unix Timestamp when DTMF Event was received by server.
