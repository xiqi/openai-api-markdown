# The transcription object (JSON)

Source: https://platform.openai.com/docs/api-reference/audio/json-object

Represents a transcription response returned by model, based on the provided input.

## Properties
- `text` (string, required): The transcribed text.
- `logprobs` (array<object>, optional): The log probabilities of the tokens in the transcription. Only returned with the models `gpt-4o-transcribe` and `gpt-4o-mini-transcribe` if `logprobs` is added to the `include` array.
  - Items:
    - `token` (string, optional): The token in the transcription.
    - `logprob` (number, optional): The log probability of the token.
    - `bytes` (array<number>, optional): The bytes of the token.
- `usage` (object, optional): Token usage statistics for the request.
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
