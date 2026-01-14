# Stream Event (transcript.text.delta)

Source: https://platform.openai.com/docs/api-reference/audio/transcript-text-delta-event

Emitted when there is an additional text delta. This is also the first event emitted when the transcription starts. Only emitted when you [create a transcription](createTranscription.md) with the `Stream` parameter set to `true`.

## Properties
- `type` (string, required): The type of the event. Always `transcript.text.delta`. Enum: 'transcript.text.delta'.
- `delta` (string, required): The text delta that was additionally transcribed.
- `logprobs` (array<object>, optional): The log probabilities of the delta. Only included if you [create a transcription](createTranscription.md) with the `include[]` parameter set to `logprobs`.
  - Items:
    - `token` (string, optional): The token that was used to generate the log probability.
    - `logprob` (number, optional): The log probability of the token.
    - `bytes` (array<integer>, optional): The bytes that were used to generate the log probability.
- `segment_id` (string, optional): Identifier of the diarized segment that this delta belongs to. Only present when using `gpt-4o-transcribe-diarize`.
