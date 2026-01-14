# response.create

Source: https://platform.openai.com/docs/api-reference/realtime-client-events/response/create

This event instructs the server to create a Response, which means triggering 
model inference. When in Server VAD mode, the server will create Responses 
automatically.

A Response will include at least one Item, and may have two, in which case 
the second will be a function call. These Items will be appended to the 
conversation history by default.

The server will respond with a `response.created` event, events for Items 
and content created, and finally a `response.done` event to indicate the 
Response is complete.

The `response.create` event includes inference configuration like 
`instructions` and `tools`. If these are set, they will override the Session's 
configuration for this Response only.

Responses can be created out-of-band of the default Conversation, meaning that they can
have arbitrary input, and it's possible to disable writing the output to the Conversation.
Only one Response can write to the default Conversation at a time, but otherwise multiple
Responses can be created in parallel. The `metadata` field is a good way to disambiguate
multiple simultaneous Responses.

Clients can set `conversation` to `none` to create a Response that does not write to the default
Conversation. Arbitrary input can be provided with the `input` field, which is an array accepting
raw Items and references to existing Items.

## Properties
- `event_id` (string, optional): Optional client-generated ID used to identify this event.
- `type` (string, required): The event type, must be `response.create`. Enum: 'response.create'.
- `response` (object, optional): Create a new Realtime response with these parameters
  - `output_modalities` (array<string>, optional): The set of modalities the model used to respond, currently the only possible values are
    `[\"audio\"]`, `[\"text\"]`. Audio output always include a text transcript. Setting the
    output to mode `text` will disable audio output from the model.
  - `instructions` (string, optional): The default system instructions (i.e. system message) prepended to model calls. This field allows the client to guide the model on desired responses. The model can be instructed on response content and format, (e.g. "be extremely succinct", "act friendly", "here are examples of good responses") and on audio behavior (e.g. "talk quickly", "inject emotion into your voice", "laugh frequently"). The instructions are not guaranteed to be followed by the model, but they provide guidance to the model on the desired behavior.
    Note that the server sets default instructions which will be used if this field is not set and are visible in the `session.created` event at the start of the session.
  - `audio` (object, optional): Configuration for audio input and output.
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
  - `conversation` (string, optional): Controls which conversation the response is added to. Currently supports
    `auto` and `none`, with `auto` as the default value. The `auto` value
    means that the contents of the response will be added to the default
    conversation. Set this to `none` to create an out-of-band response which
    will not add items to default conversation.
  - `metadata` (object | null, optional)
  - `prompt` (object | null, optional)
    - Variant (object):
      - `id` (string, required): The unique identifier of the prompt template to use.
      - `version` (string | null, optional)
      - `variables` (object | null, optional)
  - `input` (array<object>, optional): Input items to include in the prompt for the model. Using this field
    creates a new context for this Response instead of using the default
    conversation. An empty array `[]` will clear the context for this Response.
    Note that this can include references to items that previously appeared in the session
    using their id.
