# The session object

Source: https://platform.openai.com/docs/api-reference/realtime-beta-sessions/session_object

A Realtime session configuration object.

## Properties
- `id` (string, optional): Unique identifier for the session that looks like `sess_1234567890abcdef`.
- `object` (string, optional): The object type. Always `realtime.session`.
- `expires_at` (integer, optional): Expiration timestamp for the session, in seconds since epoch.
- `include` (array<string>, optional): Additional fields to include in server outputs.
  - `item.input_audio_transcription.logprobs`: Include logprobs for input audio transcription.
- `model` (string, optional): The Realtime model used for this session.
- `output_modalities` (object, optional): The set of modalities the model can respond with. To disable audio,
  set this to ["text"].
- `instructions` (string, optional): The default system instructions (i.e. system message) prepended to model
  calls. This field allows the client to guide the model on desired
  responses. The model can be instructed on response content and format,
  (e.g. "be extremely succinct", "act friendly", "here are examples of good
  responses") and on audio behavior (e.g. "talk quickly", "inject emotion
  into your voice", "laugh frequently"). The instructions are not guaranteed
  to be followed by the model, but they provide guidance to the model on the
  desired behavior.
  
  Note that the server sets default instructions which will be used if this
  field is not set and are visible in the `session.created` event at the
  start of the session.
- `audio` (object, optional): Configuration for input and output audio for the session.
  - `input` (object, optional)
    - `format` (object, optional)
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcm`. Enum: 'audio/pcm'.
        - `rate` (integer, optional): The sample rate of the audio. Always `24000`. Enum: 24000.
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcmu`. Enum: 'audio/pcmu'.
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcma`. Enum: 'audio/pcma'.
    - `transcription` (object, optional): Configuration for input audio transcription.
      - `model` (string, optional): The model to use for transcription. Current options are `whisper-1`, `gpt-4o-mini-transcribe`, `gpt-4o-mini-transcribe-2025-12-15`, `gpt-4o-transcribe`, and `gpt-4o-transcribe-diarize`. Use `gpt-4o-transcribe-diarize` when you need diarization with speaker labels.
      - `language` (string, optional): The language of the input audio. Supplying the input language in
        [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) (e.g. `en`) format
        will improve accuracy and latency.
      - `prompt` (string, optional): An optional text to guide the model's style or continue a previous audio
        segment.
        For `whisper-1`, the [prompt is a list of keywords](https://platform.openai.com/docs/guides/speech-to-text#prompting).
        For `gpt-4o-transcribe` models (excluding `gpt-4o-transcribe-diarize`), the prompt is a free text string, for example "expect words related to technology".
    - `noise_reduction` (object, optional): Configuration for input audio noise reduction.
      - `type` (string, optional): Type of noise reduction. `near_field` is for close-talking microphones such as headphones, `far_field` is for far-field microphones such as laptop or conference room microphones. Enum: 'near_field', 'far_field'.
    - `turn_detection` (object, optional): Configuration for turn detection.
      - `type` (string, optional): Type of turn detection, only `server_vad` is currently supported.
      - `threshold` (number, optional)
      - `prefix_padding_ms` (integer, optional)
      - `silence_duration_ms` (integer, optional)
  - `output` (object, optional)
    - `format` (object, optional)
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcm`. Enum: 'audio/pcm'.
        - `rate` (integer, optional): The sample rate of the audio. Always `24000`. Enum: 24000.
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcmu`. Enum: 'audio/pcmu'.
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcma`. Enum: 'audio/pcma'.
    - `voice` (string, optional)
    - `speed` (number, optional)
- `tracing` (string | object, optional): Configuration options for tracing. Set to null to disable tracing. Once
  tracing is enabled for a session, the configuration cannot be modified.
  
  `auto` will create a trace for the session with default values for the
  workflow name, group id, and metadata.
  - Variant (object):
    - `workflow_name` (string, optional): The name of the workflow to attach to this trace. This is used to
      name the trace in the traces dashboard.
    - `group_id` (string, optional): The group id to attach to this trace to enable filtering and
      grouping in the traces dashboard.
    - `metadata` (object, optional): The arbitrary metadata to attach to this trace to enable
      filtering in the traces dashboard.
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
- `tools` (array<object>, optional): Tools (functions) available to the model.
  - Items:
    - `type` (string, optional): The type of the tool, i.e. `function`. Enum: 'function'.
    - `name` (string, optional): The name of the function.
    - `description` (string, optional): The description of the function, including guidance on when and how
      to call it, and guidance about what to tell the user when calling
      (if anything).
    - `parameters` (object, optional): Parameters of the function in JSON Schema.
- `tool_choice` (string, optional): How the model chooses tools. Options are `auto`, `none`, `required`, or
  specify a function.
- `max_output_tokens` (integer | string, optional): Maximum number of output tokens for a single assistant response,
  inclusive of tool calls. Provide an integer between 1 and 4096 to
  limit output tokens, or `inf` for the maximum available tokens for a
  given model. Defaults to `inf`.
