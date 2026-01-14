# session.update

Source: https://platform.openai.com/docs/api-reference/realtime-beta-client-events/session/update

Send this event to update the session’s default configuration.
The client may send this event at any time to update any field,
except for `voice`. However, note that once a session has been
initialized with a particular `model`, it can’t be changed to
another model using `session.update`.

When the server receives a `session.update`, it will respond
with a `session.updated` event showing the full, effective configuration.
Only the fields that are present are updated. To clear a field like
`instructions`, pass an empty string.

## Properties
- `event_id` (string, optional): Optional client-generated ID used to identify this event.
- `type` (string, required): The event type, must be `session.update`. Enum: 'session.update'.
- `session` (object, required): A new Realtime session configuration, with an ephemeral key. Default TTL
  for keys is one minute.
  - `client_secret` (object, required): Ephemeral key returned by the API.
    - `value` (string, required): Ephemeral key usable in client environments to authenticate connections
      to the Realtime API. Use this in client-side environments rather than
      a standard API token, which should only be used server-side.
    - `expires_at` (integer, required): Timestamp for when the token expires. Currently, all tokens expire
      after one minute.
  - `modalities` (object, optional): The set of modalities the model can respond with. To disable audio,
    set this to ["text"].
  - `instructions` (string, optional): The default system instructions (i.e. system message) prepended to model calls. This field allows the client to guide the model on desired responses. The model can be instructed on response content and format, (e.g. "be extremely succinct", "act friendly", "here are examples of good responses") and on audio behavior (e.g. "talk quickly", "inject emotion into your voice", "laugh frequently"). The instructions are not guaranteed to be followed by the model, but they provide guidance to the model on the desired behavior.
    Note that the server sets default instructions which will be used if this field is not set and are visible in the `session.created` event at the start of the session.
  - `voice` (string | object, optional): The voice the model uses to respond. Supported built-in voices are
    `alloy`, `ash`, `ballad`, `coral`, `echo`, `sage`, `shimmer`, `verse`,
    `marin`, and `cedar`. You may also provide a custom voice object with an
    `id`, for example `{ "id": "voice_1234" }`. Voice cannot be changed during
    the session once the model has responded with audio at least once.
    - Variant (object):
      - `id` (string, required): The custom voice ID, e.g. `voice_1234`.
  - `input_audio_format` (string, optional): The format of input audio. Options are `pcm16`, `g711_ulaw`, or `g711_alaw`.
  - `output_audio_format` (string, optional): The format of output audio. Options are `pcm16`, `g711_ulaw`, or `g711_alaw`.
  - `input_audio_transcription` (object, optional): Configuration for input audio transcription, defaults to off and can be
    set to `null` to turn off once on. Input audio transcription is not native
    to the model, since the model consumes audio directly. Transcription runs
    asynchronously and should be treated as rough guidance
    rather than the representation understood by the model.
    - `model` (string, optional): The model to use for transcription.
  - `speed` (number, optional): The speed of the model's spoken response. 1.0 is the default speed. 0.25 is
    the minimum speed. 1.5 is the maximum speed. This value can only be changed
    in between model turns, not while a response is in progress. Default: `1`.
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
  - `temperature` (number, optional): Sampling temperature for the model, limited to [0.6, 1.2]. Defaults to 0.8.
  - `max_response_output_tokens` (integer | string, optional): Maximum number of output tokens for a single assistant response,
    inclusive of tool calls. Provide an integer between 1 and 4096 to
    limit output tokens, or `inf` for the maximum available tokens for a
    given model. Defaults to `inf`.
  - `truncation` (string | object, optional): When the number of tokens in a conversation exceeds the model's input token limit, the conversation be truncated, meaning messages (starting from the oldest) will not be included in the model's context. A 32k context model with 4,096 max output tokens can only include 28,224 tokens in the context before truncation occurs.
    
    Clients can configure truncation behavior to truncate with a lower max token limit, which is an effective way to control token usage and cost.
    
    Truncation will reduce the number of cached tokens on the next turn (busting the cache), since messages are dropped from the beginning of the context. However, clients can also configure truncation to retain messages up to a fraction of the maximum context size, which will reduce the need for future truncations and thus improve the cache rate.
    
    Truncation can be disabled entirely, which means the server will never truncate but would instead return an error if the conversation exceeds the model's input token limit.
    - Variant (object):
      - `type` (string, required): Use retention ratio truncation. Enum: 'retention_ratio'.
      - `retention_ratio` (number, required): Fraction of post-instruction conversation tokens to retain (`0.0` - `1.0`) when the conversation exceeds the input token limit. Setting this to `0.8` means that messages will be dropped until 80% of the maximum allowed tokens are used. This helps reduce the frequency of truncations and improve cache rates.
      - `token_limits` (object, optional): Optional custom token limits for this truncation strategy. If not provided, the model's default token limits will be used.
        - `post_instructions` (integer, optional): Maximum tokens allowed in the conversation after instructions (which including tool definitions). For example, setting this to 5,000 would mean that truncation would occur when the conversation exceeds 5,000 tokens after instructions. This cannot be higher than the model's context window size minus the maximum output tokens.
  - `prompt` (object | null, optional)
    - Variant (object):
      - `id` (string, required): The unique identifier of the prompt template to use.
      - `version` (string | null, optional)
      - `variables` (object | null, optional)
