# response.in_progress

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/in_progress

Emitted when the response is in progress.

## Properties
- `type` (string, required): The type of the event. Always `response.in_progress`. Enum: 'response.in_progress'.
- `response` (object, required): The response that is in progress.
  - `metadata` (object | null, required)
  - `top_logprobs` (integer | null, optional)
  - `temperature` (number | null, required)
  - `top_p` (number | null, required)
  - `user` (string, optional): This field is being replaced by `safety_identifier` and `prompt_cache_key`. Use `prompt_cache_key` instead to maintain caching optimizations.
    A stable identifier for your end-users.
    Used to boost cache hit rates by better bucketing similar requests and  to help OpenAI detect and prevent abuse. [Learn more](https://platform.openai.com/docs/guides/safety-best-practices#safety-identifiers). Deprecated.
  - `safety_identifier` (string, optional): A stable identifier used to help detect users of your application that may be violating OpenAI's usage policies.
    The IDs should be a string that uniquely identifies each user. We recommend hashing their username or email address, in order to avoid sending us any identifying information. [Learn more](https://platform.openai.com/docs/guides/safety-best-practices#safety-identifiers).
  - `prompt_cache_key` (string, optional): Used by OpenAI to cache responses for similar requests to optimize your cache hit rates. Replaces the `user` field. [Learn more](https://platform.openai.com/docs/guides/prompt-caching).
  - `service_tier` (string | null, optional)
  - `prompt_cache_retention` (string | null, optional)
  - `previous_response_id` (string | null, optional)
  - `model` (string, required): Model ID used to generate the response, like `gpt-4o` or `o3`. OpenAI
    offers a wide range of models with different capabilities, performance
    characteristics, and price points. Refer to the [model guide](https://platform.openai.com/docs/models)
    to browse and compare available models.
  - `reasoning` (object | null, optional)
    - Variant (object):
      - `effort` (string | null, optional)
      - `summary` (string | null, optional)
      - `generate_summary` (string | null, optional)
  - `background` (boolean | null, optional)
  - `max_output_tokens` (integer | null, optional)
  - `max_tool_calls` (integer | null, optional)
  - `text` (object, optional): Configuration options for a text response from the model. Can be plain
    text or structured JSON data. Learn more:
    - [Text inputs and outputs](https://platform.openai.com/docs/guides/text)
    - [Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)
    - `format` (object, optional): An object specifying the format that the model must output.
      
      Configuring `{ "type": "json_schema" }` enables Structured Outputs, 
      which ensures the model will match your supplied JSON schema. Learn more in the 
      [Structured Outputs guide](https://platform.openai.com/docs/guides/structured-outputs).
      
      The default format is `{ "type": "text" }` with no additional options.
      
      **Not recommended for gpt-4o and newer models:**
      
      Setting to `{ "type": "json_object" }` enables the older JSON mode, which
      ensures the message the model generates is valid JSON. Using `json_schema`
      is preferred for models that support it.
      - Variant (object):
        - `type` (string, required): The type of response format being defined. Always `text`. Enum: 'text'.
      - Variant (object):
        - `type` (string, required): The type of response format being defined. Always `json_schema`. Enum: 'json_schema'.
        - `description` (string, optional): A description of what the response format is for, used by the model to
          determine how to respond in the format.
        - `name` (string, required): The name of the response format. Must be a-z, A-Z, 0-9, or contain
          underscores and dashes, with a maximum length of 64.
        - `schema` (object, required): The schema for the response format, described as a JSON Schema object.
          Learn how to build JSON schemas [here](https://json-schema.org/).
        - `strict` (boolean | null, optional)
      - Variant (object):
        - `type` (string, required): The type of response format being defined. Always `json_object`. Enum: 'json_object'.
    - `verbosity` (string | null, optional)
  - `tools` (array<object>, required): An array of tools the model may call while generating a response. You
    can specify which tool to use by setting the `tool_choice` parameter.
    
    We support the following categories of tools:
    - **Built-in tools**: Tools that are provided by OpenAI that extend the
      model's capabilities, like [web search](https://platform.openai.com/docs/guides/tools-web-search)
      or [file search](https://platform.openai.com/docs/guides/tools-file-search). Learn more about
      [built-in tools](https://platform.openai.com/docs/guides/tools).
    - **MCP Tools**: Integrations with third-party systems via custom MCP servers
      or predefined connectors such as Google Drive and SharePoint. Learn more about
      [MCP Tools](https://platform.openai.com/docs/guides/tools-connectors-mcp).
    - **Function calls (custom tools)**: Functions that are defined by you,
      enabling the model to call your own code with strongly typed arguments
      and outputs. Learn more about
      [function calling](https://platform.openai.com/docs/guides/function-calling). You can also use
      custom tools to call your own code.
  - `tool_choice` (string | object, required): How the model should select which tool (or tools) to use when generating
    a response. See the `tools` parameter to see how to specify which tools
    the model can call.
    - Variant (object):
      - `type` (string, required): Allowed tool configuration type. Always `allowed_tools`. Enum: 'allowed_tools'.
      - `mode` (string, required): Constrains the tools available to the model to a pre-defined set.
        
        `auto` allows the model to pick from among the allowed tools and generate a
        message.
        
        `required` requires the model to call one or more of the allowed tools. Enum: 'auto', 'required'.
      - `tools` (array<object>, required): A list of tool definitions that the model should be allowed to call.
        
        For the Responses API, the list of tool definitions might look like:
        ```json
        [
          { "type": "function", "name": "get_weather" },
          { "type": "mcp", "server_label": "deepwiki" },
          { "type": "image_generation" }
        ]
        ```
    - Variant (object):
      - `type` (string, required): The type of hosted tool the model should to use. Learn more about
        [built-in tools](https://platform.openai.com/docs/guides/tools).
        
        Allowed values are:
        - `file_search`
        - `web_search_preview`
        - `computer_use_preview`
        - `code_interpreter`
        - `image_generation` Enum: 'file_search', 'web_search_preview', 'computer_use_preview', 'web_search_preview_2025_03_11', 'image_generation', 'code_interpreter'.
    - Variant (object):
      - `type` (string, required): For function calling, the type is always `function`. Enum: 'function'.
      - `name` (string, required): The name of the function to call.
    - Variant (object):
      - `type` (string, required): For MCP tools, the type is always `mcp`. Enum: 'mcp'.
      - `server_label` (string, required): The label of the MCP server to use.
      - `name` (string | null, optional)
    - Variant (object):
      - `type` (string, required): For custom tool calling, the type is always `custom`. Enum: 'custom'.
      - `name` (string, required): The name of the custom tool to call.
    - Variant (object):
      - `type` (string, required): The tool to call. Always `apply_patch`. Enum: 'apply_patch'. Default: `apply_patch`.
    - Variant (object):
      - `type` (string, required): The tool to call. Always `shell`. Enum: 'shell'. Default: `shell`.
  - `prompt` (object | null, optional)
    - Variant (object):
      - `id` (string, required): The unique identifier of the prompt template to use.
      - `version` (string | null, optional)
      - `variables` (object | null, optional)
  - `truncation` (string | null, optional)
  - `id` (string, required): Unique identifier for this Response.
  - `object` (string, required): The object type of this resource - always set to `response`. Enum: 'response'.
  - `status` (string, optional): The status of the response generation. One of `completed`, `failed`,
    `in_progress`, `cancelled`, `queued`, or `incomplete`. Enum: 'completed', 'failed', 'in_progress', 'cancelled', 'queued', 'incomplete'.
  - `created_at` (number, required): Unix timestamp (in seconds) of when this Response was created.
  - `completed_at` (number | null, optional)
  - `error` (object | null, required)
    - Variant (object):
      - `code` (string, required): The error code for the response. Enum: 'server_error', 'rate_limit_exceeded', 'invalid_prompt', 'vector_store_timeout', 'invalid_image', 'invalid_image_format', 'invalid_base64_image', 'invalid_image_url', 'image_too_large', 'image_too_small', 'image_parse_error', 'image_content_policy_violation', 'invalid_image_mode', 'image_file_too_large', 'unsupported_image_media_type', 'empty_image_file', 'failed_to_download_image', 'image_file_not_found'.
      - `message` (string, required): A human-readable description of the error.
  - `incomplete_details` (object | null, required)
    - Variant (object):
      - `reason` (string, optional): The reason why the response is incomplete. Enum: 'max_output_tokens', 'content_filter'.
  - `output` (array<object>, required): An array of content items generated by the model.
    
    - The length and order of items in the `output` array is dependent
      on the model's response.
    - Rather than accessing the first item in the `output` array and
      assuming it's an `assistant` message with the content generated by
      the model, you might consider using the `output_text` property where
      supported in SDKs.
  - `instructions` (string | array<object> | null, required)
  - `output_text` (string | null, optional)
  - `usage` (object, optional): Represents token usage details including input tokens, output tokens,
    a breakdown of output tokens, and the total tokens used.
    - `input_tokens` (integer, required): The number of input tokens.
    - `input_tokens_details` (object, required): A detailed breakdown of the input tokens.
      - `cached_tokens` (integer, required): The number of tokens that were retrieved from the cache. 
        [More on prompt caching](https://platform.openai.com/docs/guides/prompt-caching).
    - `output_tokens` (integer, required): The number of output tokens.
    - `output_tokens_details` (object, required): A detailed breakdown of the output tokens.
      - `reasoning_tokens` (integer, required): The number of reasoning tokens.
    - `total_tokens` (integer, required): The total number of tokens used.
  - `parallel_tool_calls` (boolean, required): Whether to allow the model to run tool calls in parallel. Default: `True`.
  - `conversation` (object | null, optional)
    - Variant (object):
      - `id` (string, required): The unique ID of the conversation that this response was associated with.
- `sequence_number` (integer, required): The sequence number of this event.
