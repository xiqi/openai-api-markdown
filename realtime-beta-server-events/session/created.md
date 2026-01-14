# session.created

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/session/created

Returned when a Session is created. Emitted automatically when a new
connection is established as the first server event. This event will contain
the default Session configuration.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `session.created`. Enum: 'session.created'.
- `session` (object, required): Realtime session object for the beta interface.
  - `id` (string, optional): Unique identifier for the session that looks like `sess_1234567890abcdef`.
  - `object` (string, optional): The object type. Always `realtime.session`. Enum: 'realtime.session'.
  - `modalities` (object, optional): The set of modalities the model can respond with. To disable audio,
    set this to ["text"].
  - `model` (string, optional): The Realtime model used for this session.
  - `instructions` (string, optional): The default system instructions (i.e. system message) prepended to model
    calls. This field allows the client to guide the model on desired
    responses. The model can be instructed on response content and format,
    (e.g. "be extremely succinct", "act friendly", "here are examples of good
    responses") and on audio behavior (e.g. "talk quickly", "inject emotion
    into your voice", "laugh frequently"). The instructions are not
    guaranteed to be followed by the model, but they provide guidance to the
    model on the desired behavior.
    
    
    Note that the server sets default instructions which will be used if this
    field is not set and are visible in the `session.created` event at the
    start of the session.
  - `voice` (string, optional): The voice the model uses to respond. Voice cannot be changed during the
    session once the model has responded with audio at least once. Current
    voice options are `alloy`, `ash`, `ballad`, `coral`, `echo`, `sage`,
    `shimmer`, and `verse`.
  - `input_audio_format` (string, optional): The format of input audio. Options are `pcm16`, `g711_ulaw`, or `g711_alaw`.
    For `pcm16`, input audio must be 16-bit PCM at a 24kHz sample rate,
    single channel (mono), and little-endian byte order. Enum: 'pcm16', 'g711_ulaw', 'g711_alaw'. Default: `pcm16`.
  - `output_audio_format` (string, optional): The format of output audio. Options are `pcm16`, `g711_ulaw`, or `g711_alaw`.
    For `pcm16`, output audio is sampled at a rate of 24kHz. Enum: 'pcm16', 'g711_ulaw', 'g711_alaw'. Default: `pcm16`.
  - `input_audio_transcription` (object | null, optional)
    - Variant (object):
      - `model` (string, optional): The model to use for transcription. Current options are `whisper-1`, `gpt-4o-mini-transcribe`, `gpt-4o-mini-transcribe-2025-12-15`, `gpt-4o-transcribe`, and `gpt-4o-transcribe-diarize`. Use `gpt-4o-transcribe-diarize` when you need diarization with speaker labels.
      - `language` (string, optional): The language of the input audio. Supplying the input language in
        [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) (e.g. `en`) format
        will improve accuracy and latency.
      - `prompt` (string, optional): An optional text to guide the model's style or continue a previous audio
        segment.
        For `whisper-1`, the [prompt is a list of keywords](https://platform.openai.com/docs/guides/speech-to-text#prompting).
        For `gpt-4o-transcribe` models (excluding `gpt-4o-transcribe-diarize`), the prompt is a free text string, for example "expect words related to technology".
  - `turn_detection` (object | null, optional)
  - `input_audio_noise_reduction` (object, optional): Configuration for input audio noise reduction. This can be set to `null` to turn off.
    Noise reduction filters audio added to the input audio buffer before it is sent to VAD and the model.
    Filtering the audio can improve VAD and turn detection accuracy (reducing false positives) and model performance by improving perception of the input audio.
    - `type` (string, optional): Type of noise reduction. `near_field` is for close-talking microphones such as headphones, `far_field` is for far-field microphones such as laptop or conference room microphones. Enum: 'near_field', 'far_field'.
  - `speed` (number, optional): The speed of the model's spoken response. 1.0 is the default speed. 0.25 is
    the minimum speed. 1.5 is the maximum speed. This value can only be changed
    in between model turns, not while a response is in progress. Default: `1`.
  - `tracing` (string | object | null, optional)
  - `tools` (array<object>, optional): Tools (functions) available to the model.
    - Items:
      - `type` (string, optional): The type of the tool, i.e. `function`. Enum: 'function'.
      - `name` (string, optional): The name of the function.
      - `description` (string, optional): The description of the function, including guidance on when and how
        to call it, and guidance about what to tell the user when calling
        (if anything).
      - `parameters` (object, optional): Parameters of the function in JSON Schema.
  - `tool_choice` (string, optional): How the model chooses tools. Options are `auto`, `none`, `required`, or
    specify a function. Default: `auto`.
  - `temperature` (number, optional): Sampling temperature for the model, limited to [0.6, 1.2]. For audio models a temperature of 0.8 is highly recommended for best performance. Default: `0.8`.
  - `max_response_output_tokens` (integer | string, optional): Maximum number of output tokens for a single assistant response,
    inclusive of tool calls. Provide an integer between 1 and 4096 to
    limit output tokens, or `inf` for the maximum available tokens for a
    given model. Defaults to `inf`.
  - `expires_at` (integer, optional): Expiration timestamp for the session, in seconds since epoch.
  - `prompt` (object | null | null, optional)
  - `include` (array<string> | null, optional)
