# The transcription object (Verbose JSON)

Source: https://platform.openai.com/docs/api-reference/audio/verbose-json-object

Represents a verbose json transcription response returned by model, based on the provided input.

## Properties
- `language` (string, required): The language of the input audio.
- `duration` (number, required): The duration of the input audio.
- `text` (string, required): The transcribed text.
- `words` (array<object>, optional): Extracted words and their corresponding timestamps.
  - Items:
    - `word` (string, required): The text content of the word.
    - `start` (number, required): Start time of the word in seconds.
    - `end` (number, required): End time of the word in seconds.
- `segments` (array<object>, optional): Segments of the transcribed text and their corresponding details.
  - Items:
    - `id` (integer, required): Unique identifier of the segment.
    - `seek` (integer, required): Seek offset of the segment.
    - `start` (number, required): Start time of the segment in seconds.
    - `end` (number, required): End time of the segment in seconds.
    - `text` (string, required): Text content of the segment.
    - `tokens` (array<integer>, required): Array of token IDs for the text content.
    - `temperature` (number, required): Temperature parameter used for generating the segment.
    - `avg_logprob` (number, required): Average logprob of the segment. If the value is lower than -1, consider the logprobs failed.
    - `compression_ratio` (number, required): Compression ratio of the segment. If the value is greater than 2.4, consider the compression failed.
    - `no_speech_prob` (number, required): Probability of no speech in the segment. If the value is higher than 1.0 and the `avg_logprob` is below -1, consider this segment silent.
- `usage` (object, optional): Usage statistics for models billed by audio input duration.
  - `type` (string, required): The type of the usage object. Always `duration` for this variant. Enum: 'duration'.
  - `seconds` (number, required): Duration of the input audio in seconds.
