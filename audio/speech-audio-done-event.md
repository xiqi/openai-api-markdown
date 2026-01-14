# Stream Event (speech.audio.done)

Source: https://platform.openai.com/docs/api-reference/audio/speech-audio-done-event

Emitted when the speech synthesis is complete and all audio has been streamed.

## Properties
- `type` (string, required): The type of the event. Always `speech.audio.done`. Enum: 'speech.audio.done'.
- `usage` (object, required): Token usage statistics for the request.
  - `input_tokens` (integer, required): Number of input tokens in the prompt.
  - `output_tokens` (integer, required): Number of output tokens generated.
  - `total_tokens` (integer, required): Total number of tokens used (input + output).
