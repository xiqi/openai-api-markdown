# The transcription object (Diarized JSON)

Source: https://platform.openai.com/docs/api-reference/audio/diarized-json-object

Represents a diarized transcription response returned by the model, including the combined transcript and speaker-segment annotations.

## Properties
- `task` (string, required): The type of task that was run. Always `transcribe`. Enum: 'transcribe'.
- `duration` (number, required): Duration of the input audio in seconds.
- `text` (string, required): The concatenated transcript text for the entire audio input.
- `segments` (array<object>, required): Segments of the transcript annotated with timestamps and speaker labels.
  - Items:
    - `type` (string, required): The type of the segment. Always `transcript.text.segment`. Enum: 'transcript.text.segment'.
    - `id` (string, required): Unique identifier for the segment.
    - `start` (number, required): Start timestamp of the segment in seconds.
    - `end` (number, required): End timestamp of the segment in seconds.
    - `text` (string, required): Transcript text for this segment.
    - `speaker` (string, required): Speaker label for this segment. When known speakers are provided, the label matches `known_speaker_names[]`. Otherwise speakers are labeled sequentially using capital letters (`A`, `B`, ...).
- `usage` (object, optional): Token or duration usage statistics for the request.
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
