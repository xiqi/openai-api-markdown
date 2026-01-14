# Create client secret

Source: https://platform.openai.com/docs/api-reference/realtime-sessions/create-realtime-client-secret

`POST /v1/realtime/client_secrets`

Create a Realtime client secret with an associated session configuration.

## Request body
### application/json
- `expires_after` (object, optional): Configuration for the client secret expiration. Expiration refers to the time after which
  a client secret will no longer be valid for creating sessions. The session itself may
  continue after that time once started. A secret can be used to create multiple sessions
  until it expires.
  - `anchor` (string, optional): The anchor point for the client secret expiration, meaning that `seconds` will be added to the `created_at` time of the client secret to produce an expiration timestamp. Only `created_at` is currently supported. Enum: 'created_at'. Default: `created_at`.
  - `seconds` (integer, optional): The number of seconds from the anchor point to the expiration. Select a value between `10` and `7200` (2 hours). This default to 600 seconds (10 minutes) if not specified. Default: `600`.
- `session` (object, optional): Session configuration to use for the client secret. Choose either a realtime
  session or a transcription session.
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
        - `transcription` (object, optional): Configuration for input audio transcription, defaults to off and can be set to `null` to turn off once on. Input audio transcription is not native to the model, since the model consumes audio directly. Transcription runs asynchronously through [the /audio/transcriptions endpoint](../audio/createTranscription.md) and should be treated as guidance of input audio content rather than precisely what the model heard. The client can optionally set the language and prompt for transcription, these offer additional guidance to the transcription service.
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
        - `transcription` (object, optional): Configuration for input audio transcription, defaults to off and can be set to `null` to turn off once on. Input audio transcription is not native to the model, since the model consumes audio directly. Transcription runs asynchronously through [the /audio/transcriptions endpoint](../audio/createTranscription.md) and should be treated as guidance of input audio content rather than precisely what the model heard. The client can optionally set the language and prompt for transcription, these offer additional guidance to the transcription service.
          - ...
        - `noise_reduction` (object, optional): Configuration for input audio noise reduction. This can be set to `null` to turn off.
          Noise reduction filters audio added to the input audio buffer before it is sent to VAD and the model.
          Filtering the audio can improve VAD and turn detection accuracy (reducing false positives) and model performance by improving perception of the input audio.
          - ...
        - `turn_detection` (object | null, optional)
    - `include` (array<string>, optional): Additional fields to include in server outputs.
      
      `item.input_audio_transcription.logprobs`: Include logprobs for input audio transcription.

## Responses
### 200
Client secret created successfully.
#### application/json
- `value` (string, required): The generated client secret value.
- `expires_at` (integer, required): Expiration timestamp for the client secret, in seconds since epoch.
- `session` (object, required): The session configuration for either a realtime or transcription session.
  - Variant (object):
    - `client_secret` (object, required): Ephemeral key returned by the API.
      - `value` (string, required): Ephemeral key usable in client environments to authenticate connections to the Realtime API. Use this in client-side environments rather than a standard API token, which should only be used server-side.
      - `expires_at` (integer, required): Timestamp for when the token expires. Currently, all tokens expire
        after one minute.
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
        - `transcription` (object, optional): Configuration for input audio transcription, defaults to off and can be set to `null` to turn off once on. Input audio transcription is not native to the model, since the model consumes audio directly. Transcription runs asynchronously through [the /audio/transcriptions endpoint](../audio/createTranscription.md) and should be treated as guidance of input audio content rather than precisely what the model heard. The client can optionally set the language and prompt for transcription, these offer additional guidance to the transcription service.
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
        - `voice` (string, optional): The voice the model uses to respond. Voice cannot be changed during the
          session once the model has responded with audio at least once. Current
          voice options are `alloy`, `ash`, `ballad`, `coral`, `echo`, `sage`,
          `shimmer`, `verse`, `marin`, and `cedar`. We recommend `marin` and `cedar` for
          best quality. Default: `alloy`.
        - `speed` (number, optional): The speed of the model's spoken response as a multiple of the original speed.
          1.0 is the default speed. 0.25 is the minimum speed. 1.5 is the maximum speed. This value can only be changed in between model turns, not while a response is in progress.
          
          This parameter is a post-processing adjustment to the audio after it is generated, it's
          also possible to prompt the model to speak faster or slower. Default: `1`.
    - `include` (array<string>, optional): Additional fields to include in server outputs.
      
      `item.input_audio_transcription.logprobs`: Include logprobs for input audio transcription.
    - `tracing` (string | object | null, optional)
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
    - `type` (string, required): The type of session. Always `transcription` for transcription sessions. Enum: 'transcription'.
    - `id` (string, required): Unique identifier for the session that looks like `sess_1234567890abcdef`.
    - `object` (string, required): The object type. Always `realtime.transcription_session`.
    - `expires_at` (integer, optional): Expiration timestamp for the session, in seconds since epoch.
    - `include` (array<string>, optional): Additional fields to include in server outputs.
      - `item.input_audio_transcription.logprobs`: Include logprobs for input audio transcription.
    - `audio` (object, optional): Configuration for input audio for the session.
      - `input` (object, optional)
        - `format` (object, optional)
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
        - `transcription` (object, optional): Configuration of the transcription model.
          - ...
        - `noise_reduction` (object, optional): Configuration for input audio noise reduction.
          - ...
        - `turn_detection` (object, optional): Configuration for turn detection. Can be set to `null` to turn off. Server
          VAD means that the model will detect the start and end of speech based on
          audio volume and respond at the end of user speech.
          - ...

## Returns
The created client secret and the effective session object. The client secret is a string that looks like `ek_1234`.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/realtime/client_secrets \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "expires_after": {
      "anchor": "created_at",
      "seconds": 600
    },
    "session": {
      "type": "realtime",
      "model": "gpt-realtime",
      "instructions": "You are a friendly assistant."
    }
  }'
```
#### Response
```json
{
  "value": "ek_68af296e8e408191a1120ab6383263c2",
  "expires_at": 1756310470,
  "session": {
    "type": "realtime",
    "object": "realtime.session",
    "id": "sess_C9CiUVUzUzYIssh3ELY1d",
    "model": "gpt-realtime",
    "output_modalities": [
      "audio"
    ],
    "instructions": "You are a friendly assistant.",
    "tools": [],
    "tool_choice": "auto",
    "max_output_tokens": "inf",
    "tracing": null,
    "truncation": "auto",
    "prompt": null,
    "expires_at": 0,
    "audio": {
      "input": {
        "format": {
          "type": "audio/pcm",
          "rate": 24000
        },
        "transcription": null,
        "noise_reduction": null,
        "turn_detection": {
          "type": "server_vad",
        }
      },
      "output": {
        "format": {
          "type": "audio/pcm",
          "rate": 24000
        },
        "voice": "alloy",
        "speed": 1.0
      }
    },
    "include": null
  }
}
```
