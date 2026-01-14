# Accept call

Source: https://platform.openai.com/docs/api-reference/realtime-calls/accept-call

`POST /v1/realtime/calls/{call_id}/accept`

Accept an incoming SIP call and configure the realtime session that will
handle it.

## Parameters
- `call_id` (path, string, required): The identifier for the call provided in the
  [`realtime.call.incoming`](../webhook-events/realtime/call/incoming.md)
  webhook.

## Request body
### application/json
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
        - `type` (string, optional): The audio format. Always `audio/pcm`. Enum: 'audio/pcm'.
        - `rate` (integer, optional): The sample rate of the audio. Always `24000`. Enum: 24000.
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcmu`. Enum: 'audio/pcmu'.
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcma`. Enum: 'audio/pcma'.
    - `transcription` (object, optional): Configuration for input audio transcription, defaults to off and can be set to `null` to turn off once on. Input audio transcription is not native to the model, since the model consumes audio directly. Transcription runs asynchronously through [the /audio/transcriptions endpoint](../audio/createTranscription.md) and should be treated as guidance of input audio content rather than precisely what the model heard. The client can optionally set the language and prompt for transcription, these offer additional guidance to the transcription service.
      - `model` (string, optional): The model to use for transcription. Current options are `whisper-1`, `gpt-4o-mini-transcribe`, `gpt-4o-mini-transcribe-2025-12-15`, `gpt-4o-transcribe`, and `gpt-4o-transcribe-diarize`. Use `gpt-4o-transcribe-diarize` when you need diarization with speaker labels.
      - `language` (string, optional): The language of the input audio. Supplying the input language in
        [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) (e.g. `en`) format
        will improve accuracy and latency.
      - `prompt` (string, optional): An optional text to guide the model's style or continue a previous audio
        segment.
        For `whisper-1`, the [prompt is a list of keywords](https://platform.openai.com/docs/guides/speech-to-text#prompting).
        For `gpt-4o-transcribe` models (excluding `gpt-4o-transcribe-diarize`), the prompt is a free text string, for example "expect words related to technology".
    - `noise_reduction` (object, optional): Configuration for input audio noise reduction. This can be set to `null` to turn off.
      Noise reduction filters audio added to the input audio buffer before it is sent to VAD and the model.
      Filtering the audio can improve VAD and turn detection accuracy (reducing false positives) and model performance by improving perception of the input audio.
      - `type` (string, optional): Type of noise reduction. `near_field` is for close-talking microphones such as headphones, `far_field` is for far-field microphones such as laptop or conference room microphones. Enum: 'near_field', 'far_field'.
    - `turn_detection` (object | null, optional)
  - `output` (object, optional)
    - `format` (object, optional): The format of the output audio.
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcm`. Enum: 'audio/pcm'.
        - `rate` (integer, optional): The sample rate of the audio. Always `24000`. Enum: 24000.
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcmu`. Enum: 'audio/pcmu'.
      - Variant (object):
        - `type` (string, optional): The audio format. Always `audio/pcma`. Enum: 'audio/pcma'.
    - `voice` (string | object, optional): The voice the model uses to respond. Supported built-in voices are
      `alloy`, `ash`, `ballad`, `coral`, `echo`, `sage`, `shimmer`, `verse`,
      `marin`, and `cedar`. You may also provide a custom voice object with
      an `id`, for example `{ "id": "voice_1234" }`. Voice cannot be changed
      during the session once the model has responded with audio at least once.
      We recommend `marin` and `cedar` for best quality. Default: `alloy`.
      - Variant (object):
        - `id` (string, required): The custom voice ID, e.g. `voice_1234`.
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
      - `post_instructions` (integer, optional): Maximum tokens allowed in the conversation after instructions (which including tool definitions). For example, setting this to 5,000 would mean that truncation would occur when the conversation exceeds 5,000 tokens after instructions. This cannot be higher than the model's context window size minus the maximum output tokens.
- `prompt` (object | null, optional)
  - Variant (object):
    - `id` (string, required): The unique identifier of the prompt template to use.
    - `version` (string | null, optional)
    - `variables` (object | null, optional)

## Responses
### 200
Call accepted successfully.

## Returns
Returns `200 OK` once OpenAI starts ringing the SIP leg with the supplied
session configuration.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/realtime/calls/$CALL_ID/accept \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
        "type": "realtime",
        "model": "gpt-realtime",
        "instructions": "You are Alex, a friendly concierge for Example Corp.",
      }'
```
