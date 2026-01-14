# session.updated

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/session/updated

Returned when a session is updated with a `session.update` event, unless
there is an error.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `session.updated`. Enum: 'session.updated'.
- `session` (object, required): The session configuration.
  - Variant (object):
    - `type` (string, required): The type of session to create. Always `realtime` for the Realtime API. Enum: 'realtime'.
    - `output_modalities` (array<string>, optional): The set of modalities the model can respond with. It defaults to `["audio"]`, indicating
      that the model will respond with audio plus a transcript. `["text"]` can be used to make
      the model respond with text only. It is not possible to request both `text` and `audio` at the same time. Default: `['audio']`.
    - `model` (string, optional): The Realtime model used for this session.
    - `instructions` (string, optional): The default system instructions (i.e. system message) prepended to model calls. This field allows the client to guide the model on desired responses. The model can be instructed on response content and format, (e.g. "be extremely succinct", "act friendly", "here are examples of good responses") and on audio behavior (e.g. "talk quickly", "inject emotion into your voice", "laugh frequently"). The instructions are not guaranteed to be followed by the model, but they provide guidance to the model on the desired behavior.
      
      Note that the server sets default instructions which will be used if this field is not set and are visible in the `session.created` event at the start of the session.
    - `audio` (object, optional): Configuration for input and output audio.
      - `input` (object, optional)
        - `format` (object, optional): The format of the input audio.
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
        - `transcription` (object, optional): Configuration for input audio transcription, defaults to off and can be set to `null` to turn off once on. Input audio transcription is not native to the model, since the model consumes audio directly. Transcription runs asynchronously through [the /audio/transcriptions endpoint](../../audio/createTranscription.md) and should be treated as guidance of input audio content rather than precisely what the model heard. The client can optionally set the language and prompt for transcription, these offer additional guidance to the transcription service.
          - ...
        - `noise_reduction` (object, optional): Configuration for input audio noise reduction. This can be set to `null` to turn off.
          Noise reduction filters audio added to the input audio buffer before it is sent to VAD and the model.
          Filtering the audio can improve VAD and turn detection accuracy (reducing false positives) and model performance by improving perception of the input audio.
          - ...
        - `turn_detection` (object | null, optional)
      - `output` (object, optional)
        - `format` (object, optional): The format of the output audio.
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
        - `voice` (string | object, optional): The voice the model uses to respond. Supported built-in voices are
          `alloy`, `ash`, `ballad`, `coral`, `echo`, `sage`, `shimmer`, `verse`,
          `marin`, and `cedar`. You may also provide a custom voice object with
          an `id`, for example `{ "id": "voice_1234" }`. Voice cannot be changed
          during the session once the model has responded with audio at least once.
          We recommend `marin` and `cedar` for best quality. Default: `alloy`.
          - Variant (object):
            - ...
        - `speed` (number, optional): The speed of the model's spoken response as a multiple of the original speed.
          1.0 is the default speed. 0.25 is the minimum speed. 1.5 is the maximum speed. This value can only be changed in between model turns, not while a response is in progress.
          
          This parameter is a post-processing adjustment to the audio after it is generated, it's
          also possible to prompt the model to speak faster or slower. Default: `1`.
    - `include` (array<string>, optional): Additional fields to include in server outputs.
      
      `item.input_audio_transcription.logprobs`: Include logprobs for input audio transcription.
    - `tracing` (string | object, optional): Realtime API can write session traces to the [Traces Dashboard](https://platform.openai.com/logs?api=traces). Set to null to disable tracing. Once
      tracing is enabled for a session, the configuration cannot be modified.
      
      `auto` will create a trace for the session with default values for the
      workflow name, group id, and metadata.
      - Variant (object):
        - `workflow_name` (string, optional): The name of the workflow to attach to this trace. This is used to
          name the trace in the Traces Dashboard.
        - `group_id` (string, optional): The group id to attach to this trace to enable filtering and
          grouping in the Traces Dashboard.
        - `metadata` (object, optional): The arbitrary metadata to attach to this trace to enable
          filtering in the Traces Dashboard.
    - `tools` (array<object>, optional): Tools available to the model.
    - `tool_choice` (string | object, optional): How the model chooses tools. Provide one of the string modes or force a specific
      function/MCP tool. Default: `auto`.
      - Variant (object):
        - `type` (string, required): For function calling, the type is always `function`. Enum: 'function'.
        - `name` (string, required): The name of the function to call.
      - Variant (object):
        - `type` (string, required): For MCP tools, the type is always `mcp`. Enum: 'mcp'.
        - `server_label` (string, required): The label of the MCP server to use.
        - `name` (string | null, optional)
    - `max_output_tokens` (integer | string, optional): Maximum number of output tokens for a single assistant response,
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
          - ...
    - `prompt` (object | null, optional)
      - Variant (object):
        - `id` (string, required): The unique identifier of the prompt template to use.
        - `version` (string | null, optional)
        - `variables` (object | null, optional)
  - Variant (object):
    - `type` (string, required): The type of session to create. Always `transcription` for transcription sessions. Enum: 'transcription'.
    - `audio` (object, optional): Configuration for input and output audio.
      - `input` (object, optional)
        - `format` (object, optional)
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
        - `transcription` (object, optional): Configuration for input audio transcription, defaults to off and can be set to `null` to turn off once on. Input audio transcription is not native to the model, since the model consumes audio directly. Transcription runs asynchronously through [the /audio/transcriptions endpoint](../../audio/createTranscription.md) and should be treated as guidance of input audio content rather than precisely what the model heard. The client can optionally set the language and prompt for transcription, these offer additional guidance to the transcription service.
          - ...
        - `noise_reduction` (object, optional): Configuration for input audio noise reduction. This can be set to `null` to turn off.
          Noise reduction filters audio added to the input audio buffer before it is sent to VAD and the model.
          Filtering the audio can improve VAD and turn detection accuracy (reducing false positives) and model performance by improving perception of the input audio.
          - ...
        - `turn_detection` (object | null, optional)
    - `include` (array<string>, optional): Additional fields to include in server outputs.
      
      `item.input_audio_transcription.logprobs`: Include logprobs for input audio transcription.
