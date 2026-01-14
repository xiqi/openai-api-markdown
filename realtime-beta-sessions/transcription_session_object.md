# The transcription session object

Source: https://platform.openai.com/docs/api-reference/realtime-beta-sessions/transcription_session_object

A new Realtime transcription session configuration.

When a session is created on the server via REST API, the session object
also contains an ephemeral key. Default TTL for keys is 10 minutes. This
property is not present when a session is updated via the WebSocket API.

## Properties
- `client_secret` (object, required): Ephemeral key returned by the API. Only present when the session is
  created on the server via REST API.
  - `value` (string, required): Ephemeral key usable in client environments to authenticate connections
    to the Realtime API. Use this in client-side environments rather than
    a standard API token, which should only be used server-side.
  - `expires_at` (integer, required): Timestamp for when the token expires. Currently, all tokens expire
    after one minute.
- `modalities` (object, optional): The set of modalities the model can respond with. To disable audio,
  set this to ["text"].
- `input_audio_format` (string, optional): The format of input audio. Options are `pcm16`, `g711_ulaw`, or `g711_alaw`.
- `input_audio_transcription` (object, optional): Configuration of the transcription model.
  - `model` (string, optional): The model to use for transcription. Current options are `whisper-1`, `gpt-4o-mini-transcribe`, `gpt-4o-mini-transcribe-2025-12-15`, `gpt-4o-transcribe`, and `gpt-4o-transcribe-diarize`. Use `gpt-4o-transcribe-diarize` when you need diarization with speaker labels.
  - `language` (string, optional): The language of the input audio. Supplying the input language in
    [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) (e.g. `en`) format
    will improve accuracy and latency.
  - `prompt` (string, optional): An optional text to guide the model's style or continue a previous audio
    segment.
    For `whisper-1`, the [prompt is a list of keywords](https://platform.openai.com/docs/guides/speech-to-text#prompting).
    For `gpt-4o-transcribe` models (excluding `gpt-4o-transcribe-diarize`), the prompt is a free text string, for example "expect words related to technology".
- `turn_detection` (object, optional): Configuration for turn detection. Can be set to `null` to turn off. Server
  VAD means that the model will detect the start and end of speech based on
  audio volume and respond at the end of user speech.
  - `type` (string, optional): Type of turn detection, only `server_vad` is currently supported.
  - `threshold` (number, optional): Activation threshold for VAD (0.0 to 1.0), this defaults to 0.5. A
    higher threshold will require louder audio to activate the model, and
    thus might perform better in noisy environments.
  - `prefix_padding_ms` (integer, optional): Amount of audio to include before the VAD detected speech (in
    milliseconds). Defaults to 300ms.
  - `silence_duration_ms` (integer, optional): Duration of silence to detect speech stop (in milliseconds). Defaults
    to 500ms. With shorter values the model will respond more quickly,
    but may jump in on short pauses from the user.
