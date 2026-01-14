# Stream Event (transcript.text.done)

Source: https://platform.openai.com/docs/api-reference/audio/transcript-text-done-event

Emitted when the transcription is complete. Contains the complete transcription text. Only emitted when you [create a transcription](createTranscription.md) with the `Stream` parameter set to `true`.

## Properties
- `type` (string, required): The type of the event. Always `transcript.text.done`. Enum: 'transcript.text.done'.
- `text` (string, required): The text that was transcribed.
- `logprobs` (array<object>, optional): The log probabilities of the individual tokens in the transcription. Only included if you [create a transcription](createTranscription.md) with the `include[]` parameter set to `logprobs`.
  - Items:
    - `token` (string, optional): The token that was used to generate the log probability.
    - `logprob` (number, optional): The log probability of the token.
    - `bytes` (array<integer>, optional): The bytes that were used to generate the log probability.
- `usage` (object, optional): Usage statistics for models billed by token usage.
  - `type` (string, required): The type of the usage object. Always `tokens` for this variant. Enum: 'tokens'.
  - `input_tokens` (integer, required): Number of input tokens billed for this request.
  - `input_token_details` (object, optional): Details about the input tokens billed for this request.
    - `text_tokens` (integer, optional): Number of text tokens billed for this request.
    - `audio_tokens` (integer, optional): Number of audio tokens billed for this request.
  - `output_tokens` (integer, required): Number of output tokens generated.
  - `total_tokens` (integer, required): Total number of tokens used (input + output).
