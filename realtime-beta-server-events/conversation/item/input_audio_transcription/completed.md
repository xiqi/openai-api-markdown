# conversation.item.input_audio_transcription.completed

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/conversation/item/input_audio_transcription/completed

This event is the output of audio transcription for user audio written to the
user audio buffer. Transcription begins when the input audio buffer is
committed by the client or server (in `server_vad` mode). Transcription runs
asynchronously with Response creation, so this event may come before or after
the Response events.

Realtime API models accept audio natively, and thus input transcription is a
separate process run on a separate ASR (Automatic Speech Recognition) model.
The transcript may diverge somewhat from the model's interpretation, and
should be treated as a rough guide.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be
  `conversation.item.input_audio_transcription.completed`. Enum: 'conversation.item.input_audio_transcription.completed'.
- `item_id` (string, required): The ID of the user message item containing the audio.
- `content_index` (integer, required): The index of the content part containing the audio.
- `transcript` (string, required): The transcribed text.
- `logprobs` (array<object> | null, optional)
- `usage` (object, required): Usage statistics for the transcription.
  - Variant (object):
    - `type` (string, required): The type of the usage object. Always `tokens` for this variant. Enum: 'tokens'.
    - `input_tokens` (integer, required): Number of input tokens billed for this request.
    - `input_token_details` (object, optional): Details about the input tokens billed for this request.
      - `text_tokens` (integer, optional): Number of text tokens billed for this request.
      - `audio_tokens` (integer, optional): Number of audio tokens billed for this request.
    - `output_tokens` (integer, required): Number of output tokens generated.
    - `total_tokens` (integer, required): Total number of tokens used (input + output).
  - Variant (object):
    - `type` (string, required): The type of the usage object. Always `duration` for this variant. Enum: 'duration'.
    - `seconds` (number, required): Duration of the input audio in seconds.
