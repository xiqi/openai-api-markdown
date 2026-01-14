# Stream Event (transcript.text.segment)

Source: https://platform.openai.com/docs/api-reference/audio/transcript-text-segment-event

Emitted when a diarized transcription returns a completed segment with speaker information. Only emitted when you [create a transcription](createTranscription.md) with `stream` set to `true` and `response_format` set to `diarized_json`.

## Properties
- `type` (string, required): The type of the event. Always `transcript.text.segment`. Enum: 'transcript.text.segment'.
- `id` (string, required): Unique identifier for the segment.
- `start` (number, required): Start timestamp of the segment in seconds.
- `end` (number, required): End timestamp of the segment in seconds.
- `text` (string, required): Transcript text for this segment.
- `speaker` (string, required): Speaker label for this segment.
