# Create a model response

Source: https://platform.openai.com/docs/api-reference/responses/create

`POST /v1/responses`

Creates a model response. Provide [text](https://platform.openai.com/docs/guides/text) or
[image](https://platform.openai.com/docs/guides/images) inputs to generate [text](https://platform.openai.com/docs/guides/text)
or [JSON](https://platform.openai.com/docs/guides/structured-outputs) outputs. Have the model call
your own [custom code](https://platform.openai.com/docs/guides/function-calling) or use built-in
[tools](https://platform.openai.com/docs/guides/tools) like [web search](https://platform.openai.com/docs/guides/tools-web-search)
or [file search](https://platform.openai.com/docs/guides/tools-file-search) to use your own data
as input for the model's response.

## Request body
### application/json
- `metadata` (object | null, optional)
- `top_logprobs` (integer, optional): An integer between 0 and 20 specifying the number of most likely tokens to
  return at each token position, each with an associated log probability.
- `temperature` (number | null, optional)
- `top_p` (number | null, optional)
- `user` (string, optional): This field is being replaced by `safety_identifier` and `prompt_cache_key`. Use `prompt_cache_key` instead to maintain caching optimizations.
  A stable identifier for your end-users.
  Used to boost cache hit rates by better bucketing similar requests and  to help OpenAI detect and prevent abuse. [Learn more](https://platform.openai.com/docs/guides/safety-best-practices#safety-identifiers). Deprecated.
- `safety_identifier` (string, optional): A stable identifier used to help detect users of your application that may be violating OpenAI's usage policies.
  The IDs should be a string that uniquely identifies each user. We recommend hashing their username or email address, in order to avoid sending us any identifying information. [Learn more](https://platform.openai.com/docs/guides/safety-best-practices#safety-identifiers).
- `prompt_cache_key` (string, optional): Used by OpenAI to cache responses for similar requests to optimize your cache hit rates. Replaces the `user` field. [Learn more](https://platform.openai.com/docs/guides/prompt-caching).
- `service_tier` (string | null, optional)
- `prompt_cache_retention` (string | null, optional)
- `previous_response_id` (string | null, optional)
- `model` (string, optional): Model ID used to generate the response, like `gpt-4o` or `o3`. OpenAI
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
- `tools` (array<object>, optional): An array of tools the model may call while generating a response. You
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
- `tool_choice` (string | object, optional): How the model should select which tool (or tools) to use when generating
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
- `input` (string | array<object>, optional): Text, image, or file inputs to the model, used to generate a response.
  
  Learn more:
  - [Text inputs and outputs](https://platform.openai.com/docs/guides/text)
  - [Image inputs](https://platform.openai.com/docs/guides/images)
  - [File inputs](https://platform.openai.com/docs/guides/pdf-files)
  - [Conversation state](https://platform.openai.com/docs/guides/conversation-state)
  - [Function calling](https://platform.openai.com/docs/guides/function-calling)
- `include` (array<string> | null, optional)
- `parallel_tool_calls` (boolean | null, optional)
- `store` (boolean | null, optional)
- `instructions` (string | null, optional)
- `stream` (boolean | null, optional)
- `stream_options` (object | null, optional)
  - Variant (object):
    - `include_obfuscation` (boolean, optional): When true, stream obfuscation will be enabled. Stream obfuscation adds
      random characters to an `obfuscation` field on streaming delta events to
      normalize payload sizes as a mitigation to certain side-channel attacks.
      These obfuscation fields are included by default, but add a small amount
      of overhead to the data stream. You can set `include_obfuscation` to
      false to optimize for bandwidth if you trust the network links between
      your application and the OpenAI API.
- `conversation` (string | object | null, optional)

## Responses
### 200
OK
#### application/json
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

Example:
```json
{
  "id": "resp_67ccd3a9da748190baa7f1570fe91ac604becb25c45c1d41",
  "object": "response",
  "created_at": 1741476777,
  "status": "completed",
  "completed_at": 1741476778,
  "error": null,
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "model": "gpt-4o-2024-08-06",
  "output": [
    {
      "type": "message",
      "id": "msg_67ccd3acc8d48190a77525dc6de64b4104becb25c45c1d41",
      "status": "completed",
      "role": "assistant",
      "content": [
        {
          "type": "output_text",
          "text": "The image depicts a scenic landscape with a wooden boardwalk or pathway leading through lush, green grass under a blue sky with some clouds. The setting suggests a peaceful natural area, possibly a park or nature reserve. There are trees and shrubs in the background.",
          "annotations": []
        }
      ]
    }
  ],
  "parallel_tool_calls": true,
  "previous_response_id": null,
  "reasoning": {
    "effort": null,
    "summary": null
  },
  "store": true,
  "temperature": 1,
  "text": {
    "format": {
      "type": "text"
    }
  },
  "tool_choice": "auto",
  "tools": [],
  "top_p": 1,
  "truncation": "disabled",
  "usage": {
    "input_tokens": 328,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens": 52,
    "output_tokens_details": {
      "reasoning_tokens": 0
    },
    "total_tokens": 380
  },
  "user": null,
  "metadata": {}
}
```
#### text/event-stream
- Schema type: `object`

## Returns
Returns a [Response](object.md) object.

## Examples
### Text input
#### Request (curl)
```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4.1",
    "input": "Tell me a three sentence bedtime story about a unicorn."
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4.1",
    input: "Tell me a three sentence bedtime story about a unicorn."
});

console.log(response);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
  model="gpt-4.1",
  input="Tell me a three sentence bedtime story about a unicorn."
)

print(response)
```
#### Request (csharp)
```csharp
using System;
using OpenAI.Responses;

OpenAIResponseClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

OpenAIResponse response = client.CreateResponse("Tell me a three sentence bedtime story about a unicorn.");

Console.WriteLine(response.GetOutputText());
```
#### Response
```json
{
  "id": "resp_67ccd2bed1ec8190b14f964abc0542670bb6a6b452d3795b",
  "object": "response",
  "created_at": 1741476542,
  "status": "completed",
  "completed_at": 1741476543,
  "error": null,
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "model": "gpt-4.1-2025-04-14",
  "output": [
    {
      "type": "message",
      "id": "msg_67ccd2bf17f0819081ff3bb2cf6508e60bb6a6b452d3795b",
      "status": "completed",
      "role": "assistant",
      "content": [
        {
          "type": "output_text",
          "text": "In a peaceful grove beneath a silver moon, a unicorn named Lumina discovered a hidden pool that reflected the stars. As she dipped her horn into the water, the pool began to shimmer, revealing a pathway to a magical realm of endless night skies. Filled with wonder, Lumina whispered a wish for all who dream to find their own hidden magic, and as she glanced back, her hoofprints sparkled like stardust.",
          "annotations": []
        }
      ]
    }
  ],
  "parallel_tool_calls": true,
  "previous_response_id": null,
  "reasoning": {
    "effort": null,
    "summary": null
  },
  "store": true,
  "temperature": 1.0,
  "text": {
    "format": {
      "type": "text"
    }
  },
  "tool_choice": "auto",
  "tools": [],
  "top_p": 1.0,
  "truncation": "disabled",
  "usage": {
    "input_tokens": 36,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens": 87,
    "output_tokens_details": {
      "reasoning_tokens": 0
    },
    "total_tokens": 123
  },
  "user": null,
  "metadata": {}
}
```
### Image input
#### Request (curl)
```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4.1",
    "input": [
      {
        "role": "user",
        "content": [
          {"type": "input_text", "text": "what is in this image?"},
          {
            "type": "input_image",
            "image_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg"
          }
        ]
      }
    ]
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4.1",
    input: [
        {
            role: "user",
            content: [
                { type: "input_text", text: "what is in this image?" },
                {
                    type: "input_image",
                    image_url:
                        "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
                },
            ],
        },
    ],
});

console.log(response);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4.1",
    input=[
        {
            "role": "user",
            "content": [
                { "type": "input_text", "text": "what is in this image?" },
                {
                    "type": "input_image",
                    "image_url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg"
                }
            ]
        }
    ]
)

print(response)
```
#### Request (csharp)
```csharp
using System;
using System.Collections.Generic;

using OpenAI.Responses;

OpenAIResponseClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

List<ResponseItem> inputItems =
[
    ResponseItem.CreateUserMessageItem(
        [
            ResponseContentPart.CreateInputTextPart("What is in this image?"),
            ResponseContentPart.CreateInputImagePart(new Uri("https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg"))
        ]
    )
];

OpenAIResponse response = client.CreateResponse(inputItems);

Console.WriteLine(response.GetOutputText());
```
#### Response
```json
{
  "id": "resp_67ccd3a9da748190baa7f1570fe91ac604becb25c45c1d41",
  "object": "response",
  "created_at": 1741476777,
  "status": "completed",
  "completed_at": 1741476778,
  "error": null,
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "model": "gpt-4.1-2025-04-14",
  "output": [
    {
      "type": "message",
      "id": "msg_67ccd3acc8d48190a77525dc6de64b4104becb25c45c1d41",
      "status": "completed",
      "role": "assistant",
      "content": [
        {
          "type": "output_text",
          "text": "The image depicts a scenic landscape with a wooden boardwalk or pathway leading through lush, green grass under a blue sky with some clouds. The setting suggests a peaceful natural area, possibly a park or nature reserve. There are trees and shrubs in the background.",
          "annotations": []
        }
      ]
    }
  ],
  "parallel_tool_calls": true,
  "previous_response_id": null,
  "reasoning": {
    "effort": null,
    "summary": null
  },
  "store": true,
  "temperature": 1.0,
  "text": {
    "format": {
      "type": "text"
    }
  },
  "tool_choice": "auto",
  "tools": [],
  "top_p": 1.0,
  "truncation": "disabled",
  "usage": {
    "input_tokens": 328,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens": 52,
    "output_tokens_details": {
      "reasoning_tokens": 0
    },
    "total_tokens": 380
  },
  "user": null,
  "metadata": {}
}
```
### File input
#### Request (curl)
```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4.1",
    "input": [
      {
        "role": "user",
        "content": [
          {"type": "input_text", "text": "what is in this file?"},
          {
            "type": "input_file",
            "file_url": "https://www.berkshirehathaway.com/letters/2024ltr.pdf"
          }
        ]
      }
    ]
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4.1",
    input: [
        {
            role: "user",
            content: [
                { type: "input_text", text: "what is in this file?" },
                {
                    type: "input_file",
                    file_url: "https://www.berkshirehathaway.com/letters/2024ltr.pdf",
                },
            ],
        },
    ],
});

console.log(response);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4.1",
    input=[
        {
            "role": "user",
            "content": [
                { "type": "input_text", "text": "what is in this file?" },
                {
                    "type": "input_file",
                    "file_url": "https://www.berkshirehathaway.com/letters/2024ltr.pdf"
                }
            ]
        }
    ]
)

print(response)
```
#### Response
```json
{
  "id": "resp_686eef60237881a2bd1180bb8b13de430e34c516d176ff86",
  "object": "response",
  "created_at": 1752100704,
  "status": "completed",
  "completed_at": 1752100705,
  "background": false,
  "error": null,
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "max_tool_calls": null,
  "model": "gpt-4.1-2025-04-14",
  "output": [
    {
      "id": "msg_686eef60d3e081a29283bdcbc4322fd90e34c516d176ff86",
      "type": "message",
      "status": "completed",
      "content": [
        {
          "type": "output_text",
          "annotations": [],
          "logprobs": [],
          "text": "The file seems to contain excerpts from a letter to the shareholders of Berkshire Hathaway Inc., likely written by Warren Buffett. It covers several topics:\n\n1. **Communication Philosophy**: Buffett emphasizes the importance of transparency and candidness in reporting mistakes and successes to shareholders.\n\n2. **Mistakes and Learnings**: The letter acknowledges past mistakes in business assessments and management hires, highlighting the importance of correcting errors promptly.\n\n3. **CEO Succession**: Mention of Greg Abel stepping in as the new CEO and continuing the tradition of honest communication.\n\n4. **Pete Liegl Story**: A detailed account of acquiring Forest River and the relationship with its founder, highlighting trust and effective business decisions.\n\n5. **2024 Performance**: Overview of business performance, particularly in insurance and investment activities, with a focus on GEICO's improvement.\n\n6. **Tax Contributions**: Discussion of significant tax payments to the U.S. Treasury, credited to shareholders' reinvestments.\n\n7. **Investment Strategy**: A breakdown of Berkshire\u2019s investments in both controlled subsidiaries and marketable equities, along with a focus on long-term holding strategies.\n\n8. **American Capitalism**: Reflections on America\u2019s economic development and Berkshire\u2019s role within it.\n\n9. **Property-Casualty Insurance**: Insights into the P/C insurance business model and its challenges and benefits.\n\n10. **Japanese Investments**: Information about Berkshire\u2019s investments in Japanese companies and future plans.\n\n11. **Annual Meeting**: Details about the upcoming annual gathering in Omaha, including schedule changes and new book releases.\n\n12. **Personal Anecdotes**: Light-hearted stories about family and interactions, conveying Buffett's personable approach.\n\n13. **Financial Performance Data**: Tables comparing Berkshire\u2019s annual performance to the S&P 500, showing impressive long-term gains.\n\nOverall, the letter reinforces Berkshire Hathaway's commitment to transparency, investment in both its businesses and the wider economy, and emphasizes strong leadership and prudent financial management."
        }
      ],
      "role": "assistant"
    }
  ],
  "parallel_tool_calls": true,
  "previous_response_id": null,
  "reasoning": {
    "effort": null,
    "summary": null
  },
  "service_tier": "default",
  "store": true,
  "temperature": 1.0,
  "text": {
    "format": {
      "type": "text"
    }
  },
  "tool_choice": "auto",
  "tools": [],
  "top_logprobs": 0,
  "top_p": 1.0,
  "truncation": "disabled",
  "usage": {
    "input_tokens": 8438,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens": 398,
    "output_tokens_details": {
      "reasoning_tokens": 0
    },
    "total_tokens": 8836
  },
  "user": null,
  "metadata": {}
}
```
### Web search
#### Request (curl)
```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4.1",
    "tools": [{ "type": "web_search_preview" }],
    "input": "What was a positive news story from today?"
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4.1",
    tools: [{ type: "web_search_preview" }],
    input: "What was a positive news story from today?",
});

console.log(response);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4.1",
    tools=[{ "type": "web_search_preview" }],
    input="What was a positive news story from today?",
)

print(response)
```
#### Request (csharp)
```csharp
using System;

using OpenAI.Responses;

OpenAIResponseClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

string userInputText = "What was a positive news story from today?";

ResponseCreationOptions options = new()
{
    Tools =
    {
        ResponseTool.CreateWebSearchTool()
    },
};

OpenAIResponse response = client.CreateResponse(userInputText, options);

Console.WriteLine(response.GetOutputText());
```
#### Response
```json
{
  "id": "resp_67ccf18ef5fc8190b16dbee19bc54e5f087bb177ab789d5c",
  "object": "response",
  "created_at": 1741484430,
  "status": "completed",
  "completed_at": 1741484431,
  "error": null,
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "model": "gpt-4.1-2025-04-14",
  "output": [
    {
      "type": "web_search_call",
      "id": "ws_67ccf18f64008190a39b619f4c8455ef087bb177ab789d5c",
      "status": "completed"
    },
    {
      "type": "message",
      "id": "msg_67ccf190ca3881909d433c50b1f6357e087bb177ab789d5c",
      "status": "completed",
      "role": "assistant",
      "content": [
        {
          "type": "output_text",
          "text": "As of today, March 9, 2025, one notable positive news story...",
          "annotations": [
            {
              "type": "url_citation",
              "start_index": 442,
              "end_index": 557,
              "url": "https://.../?utm_source=chatgpt.com",
              "title": "..."
            },
            {
              "type": "url_citation",
              "start_index": 962,
              "end_index": 1077,
              "url": "https://.../?utm_source=chatgpt.com",
              "title": "..."
            },
            {
              "type": "url_citation",
              "start_index": 1336,
              "end_index": 1451,
              "url": "https://.../?utm_source=chatgpt.com",
              "title": "..."
            }
          ]
        }
      ]
    }
  ],
  "parallel_tool_calls": true,
  "previous_response_id": null,
  "reasoning": {
    "effort": null,
    "summary": null
  },
  "store": true,
  "temperature": 1.0,
  "text": {
    "format": {
      "type": "text"
    }
  },
  "tool_choice": "auto",
  "tools": [
    {
      "type": "web_search_preview",
      "domains": [],
      "search_context_size": "medium",
      "user_location": {
        "type": "approximate",
        "city": null,
        "country": "US",
        "region": null,
        "timezone": null
      }
    }
  ],
  "top_p": 1.0,
  "truncation": "disabled",
  "usage": {
    "input_tokens": 328,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens": 356,
    "output_tokens_details": {
      "reasoning_tokens": 0
    },
    "total_tokens": 684
  },
  "user": null,
  "metadata": {}
}
```
### File search
#### Request (curl)
```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4.1",
    "tools": [{
      "type": "file_search",
      "vector_store_ids": ["vs_1234567890"],
      "max_num_results": 20
    }],
    "input": "What are the attributes of an ancient brown dragon?"
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4.1",
    tools: [{
      type: "file_search",
      vector_store_ids: ["vs_1234567890"],
      max_num_results: 20
    }],
    input: "What are the attributes of an ancient brown dragon?",
});

console.log(response);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-4.1",
    tools=[{
      "type": "file_search",
      "vector_store_ids": ["vs_1234567890"],
      "max_num_results": 20
    }],
    input="What are the attributes of an ancient brown dragon?",
)

print(response)
```
#### Request (csharp)
```csharp
using System;

using OpenAI.Responses;

OpenAIResponseClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

string userInputText = "What are the attributes of an ancient brown dragon?";

ResponseCreationOptions options = new()
{
    Tools =
    {
        ResponseTool.CreateFileSearchTool(
            vectorStoreIds: ["vs_1234567890"],
            maxResultCount: 20
        )
    },
};

OpenAIResponse response = client.CreateResponse(userInputText, options);

Console.WriteLine(response.GetOutputText());
```
#### Response
```json
{
  "id": "resp_67ccf4c55fc48190b71bd0463ad3306d09504fb6872380d7",
  "object": "response",
  "created_at": 1741485253,
  "status": "completed",
  "completed_at": 1741485254,
  "error": null,
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "model": "gpt-4.1-2025-04-14",
  "output": [
    {
      "type": "file_search_call",
      "id": "fs_67ccf4c63cd08190887ef6464ba5681609504fb6872380d7",
      "status": "completed",
      "queries": [
        "attributes of an ancient brown dragon"
      ],
      "results": null
    },
    {
      "type": "message",
      "id": "msg_67ccf4c93e5c81909d595b369351a9d309504fb6872380d7",
      "status": "completed",
      "role": "assistant",
      "content": [
        {
          "type": "output_text",
          "text": "The attributes of an ancient brown dragon include...",
          "annotations": [
            {
              "type": "file_citation",
              "index": 320,
              "file_id": "file-4wDz5b167pAf72nx1h9eiN",
              "filename": "dragons.pdf"
            },
            {
              "type": "file_citation",
              "index": 576,
              "file_id": "file-4wDz5b167pAf72nx1h9eiN",
              "filename": "dragons.pdf"
            },
            {
              "type": "file_citation",
              "index": 815,
              "file_id": "file-4wDz5b167pAf72nx1h9eiN",
              "filename": "dragons.pdf"
            },
            {
              "type": "file_citation",
              "index": 815,
              "file_id": "file-4wDz5b167pAf72nx1h9eiN",
              "filename": "dragons.pdf"
            },
            {
              "type": "file_citation",
              "index": 1030,
              "file_id": "file-4wDz5b167pAf72nx1h9eiN",
              "filename": "dragons.pdf"
            },
            {
              "type": "file_citation",
              "index": 1030,
              "file_id": "file-4wDz5b167pAf72nx1h9eiN",
              "filename": "dragons.pdf"
            },
            {
              "type": "file_citation",
              "index": 1156,
              "file_id": "file-4wDz5b167pAf72nx1h9eiN",
              "filename": "dragons.pdf"
            },
            {
              "type": "file_citation",
              "index": 1225,
              "file_id": "file-4wDz5b167pAf72nx1h9eiN",
              "filename": "dragons.pdf"
            }
          ]
        }
      ]
    }
  ],
  "parallel_tool_calls": true,
  "previous_response_id": null,
  "reasoning": {
    "effort": null,
    "summary": null
  },
  "store": true,
  "temperature": 1.0,
  "text": {
    "format": {
      "type": "text"
    }
  },
  "tool_choice": "auto",
  "tools": [
    {
      "type": "file_search",
      "filters": null,
      "max_num_results": 20,
      "ranking_options": {
        "ranker": "auto",
        "score_threshold": 0.0
      },
      "vector_store_ids": [
        "vs_1234567890"
      ]
    }
  ],
  "top_p": 1.0,
  "truncation": "disabled",
  "usage": {
    "input_tokens": 18307,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens": 348,
    "output_tokens_details": {
      "reasoning_tokens": 0
    },
    "total_tokens": 18655
  },
  "user": null,
  "metadata": {}
}
```
### Streaming
#### Request (curl)
```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4.1",
    "instructions": "You are a helpful assistant.",
    "input": "Hello!",
    "stream": true
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const response = await openai.responses.create({
    model: "gpt-4.1",
    instructions: "You are a helpful assistant.",
    input: "Hello!",
    stream: true,
});

for await (const event of response) {
    console.log(event);
}
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
  model="gpt-4.1",
  instructions="You are a helpful assistant.",
  input="Hello!",
  stream=True
)

for event in response:
  print(event)
```
#### Request (csharp)
```csharp
using System;
using System.ClientModel;
using System.Threading.Tasks;

using OpenAI.Responses;

OpenAIResponseClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

string userInputText = "Hello!";

ResponseCreationOptions options = new()
{
    Instructions = "You are a helpful assistant.",
};

AsyncCollectionResult<StreamingResponseUpdate> responseUpdates = client.CreateResponseStreamingAsync(userInputText, options);

await foreach (StreamingResponseUpdate responseUpdate in responseUpdates)
{
    if (responseUpdate is StreamingResponseOutputTextDeltaUpdate outputTextDeltaUpdate)
    {
        Console.Write(outputTextDeltaUpdate.Delta);
    }
}
```
#### Response
```json
event: response.created
data: {"type":"response.created","response":{"id":"resp_67c9fdcecf488190bdd9a0409de3a1ec07b8b0ad4e5eb654","object":"response","created_at":1741290958,"status":"in_progress","error":null,"incomplete_details":null,"instructions":"You are a helpful assistant.","max_output_tokens":null,"model":"gpt-4.1-2025-04-14","output":[],"parallel_tool_calls":true,"previous_response_id":null,"reasoning":{"effort":null,"summary":null},"store":true,"temperature":1.0,"text":{"format":{"type":"text"}},"tool_choice":"auto","tools":[],"top_p":1.0,"truncation":"disabled","usage":null,"user":null,"metadata":{}}}

event: response.in_progress
data: {"type":"response.in_progress","response":{"id":"resp_67c9fdcecf488190bdd9a0409de3a1ec07b8b0ad4e5eb654","object":"response","created_at":1741290958,"status":"in_progress","error":null,"incomplete_details":null,"instructions":"You are a helpful assistant.","max_output_tokens":null,"model":"gpt-4.1-2025-04-14","output":[],"parallel_tool_calls":true,"previous_response_id":null,"reasoning":{"effort":null,"summary":null},"store":true,"temperature":1.0,"text":{"format":{"type":"text"}},"tool_choice":"auto","tools":[],"top_p":1.0,"truncation":"disabled","usage":null,"user":null,"metadata":{}}}

event: response.output_item.added
data: {"type":"response.output_item.added","output_index":0,"item":{"id":"msg_67c9fdcf37fc8190ba82116e33fb28c507b8b0ad4e5eb654","type":"message","status":"in_progress","role":"assistant","content":[]}}

event: response.content_part.added
data: {"type":"response.content_part.added","item_id":"msg_67c9fdcf37fc8190ba82116e33fb28c507b8b0ad4e5eb654","output_index":0,"content_index":0,"part":{"type":"output_text","text":"","annotations":[]}}

event: response.output_text.delta
data: {"type":"response.output_text.delta","item_id":"msg_67c9fdcf37fc8190ba82116e33fb28c507b8b0ad4e5eb654","output_index":0,"content_index":0,"delta":"Hi"}

...

event: response.output_text.done
data: {"type":"response.output_text.done","item_id":"msg_67c9fdcf37fc8190ba82116e33fb28c507b8b0ad4e5eb654","output_index":0,"content_index":0,"text":"Hi there! How can I assist you today?"}

event: response.content_part.done
data: {"type":"response.content_part.done","item_id":"msg_67c9fdcf37fc8190ba82116e33fb28c507b8b0ad4e5eb654","output_index":0,"content_index":0,"part":{"type":"output_text","text":"Hi there! How can I assist you today?","annotations":[]}}

event: response.output_item.done
data: {"type":"response.output_item.done","output_index":0,"item":{"id":"msg_67c9fdcf37fc8190ba82116e33fb28c507b8b0ad4e5eb654","type":"message","status":"completed","role":"assistant","content":[{"type":"output_text","text":"Hi there! How can I assist you today?","annotations":[]}]}}

event: response.completed
data: {"type":"response.completed","response":{"id":"resp_67c9fdcecf488190bdd9a0409de3a1ec07b8b0ad4e5eb654","object":"response","created_at":1741290958,"status":"completed","error":null,"incomplete_details":null,"instructions":"You are a helpful assistant.","max_output_tokens":null,"model":"gpt-4.1-2025-04-14","output":[{"id":"msg_67c9fdcf37fc8190ba82116e33fb28c507b8b0ad4e5eb654","type":"message","status":"completed","role":"assistant","content":[{"type":"output_text","text":"Hi there! How can I assist you today?","annotations":[]}]}],"parallel_tool_calls":true,"previous_response_id":null,"reasoning":{"effort":null,"summary":null},"store":true,"temperature":1.0,"text":{"format":{"type":"text"}},"tool_choice":"auto","tools":[],"top_p":1.0,"truncation":"disabled","usage":{"input_tokens":37,"output_tokens":11,"output_tokens_details":{"reasoning_tokens":0},"total_tokens":48},"user":null,"metadata":{}}}
```
### Functions
#### Request (curl)
```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4.1",
    "input": "What is the weather like in Boston today?",
    "tools": [
      {
        "type": "function",
        "name": "get_current_weather",
        "description": "Get the current weather in a given location",
        "parameters": {
          "type": "object",
          "properties": {
            "location": {
              "type": "string",
              "description": "The city and state, e.g. San Francisco, CA"
            },
            "unit": {
              "type": "string",
              "enum": ["celsius", "fahrenheit"]
            }
          },
          "required": ["location", "unit"]
        }
      }
    ],
    "tool_choice": "auto"
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const tools = [
    {
        type: "function",
        name: "get_current_weather",
        description: "Get the current weather in a given location",
        parameters: {
            type: "object",
            properties: {
                location: {
                    type: "string",
                    description: "The city and state, e.g. San Francisco, CA",
                },
                unit: { type: "string", enum: ["celsius", "fahrenheit"] },
            },
            required: ["location", "unit"],
        },
    },
];

const response = await openai.responses.create({
    model: "gpt-4.1",
    tools: tools,
    input: "What is the weather like in Boston today?",
    tool_choice: "auto",
});

console.log(response);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

tools = [
    {
        "type": "function",
        "name": "get_current_weather",
        "description": "Get the current weather in a given location",
        "parameters": {
          "type": "object",
          "properties": {
              "location": {
                  "type": "string",
                  "description": "The city and state, e.g. San Francisco, CA",
              },
              "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]},
          },
          "required": ["location", "unit"],
        }
    }
]

response = client.responses.create(
  model="gpt-4.1",
  tools=tools,
  input="What is the weather like in Boston today?",
  tool_choice="auto"
)

print(response)
```
#### Request (csharp)
```csharp
using System;
using OpenAI.Responses;

OpenAIResponseClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

ResponseTool getCurrentWeatherFunctionTool = ResponseTool.CreateFunctionTool(
    functionName: "get_current_weather",
    functionDescription: "Get the current weather in a given location",
    functionParameters: BinaryData.FromString("""
        {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "The city and state, e.g. San Francisco, CA"
                },
                "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]}
            },
            "required": ["location", "unit"]
        }
        """
    )
);

string userInputText = "What is the weather like in Boston today?";

ResponseCreationOptions options = new()
{
    Tools =
    {
        getCurrentWeatherFunctionTool
    },
    ToolChoice = ResponseToolChoice.CreateAutoChoice(),
};

OpenAIResponse response = client.CreateResponse(userInputText, options);
```
#### Response
```json
{
  "id": "resp_67ca09c5efe0819096d0511c92b8c890096610f474011cc0",
  "object": "response",
  "created_at": 1741294021,
  "status": "completed",
  "completed_at": 1741294022,
  "error": null,
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "model": "gpt-4.1-2025-04-14",
  "output": [
    {
      "type": "function_call",
      "id": "fc_67ca09c6bedc8190a7abfec07b1a1332096610f474011cc0",
      "call_id": "call_unLAR8MvFNptuiZK6K6HCy5k",
      "name": "get_current_weather",
      "arguments": "{\"location\":\"Boston, MA\",\"unit\":\"celsius\"}",
      "status": "completed"
    }
  ],
  "parallel_tool_calls": true,
  "previous_response_id": null,
  "reasoning": {
    "effort": null,
    "summary": null
  },
  "store": true,
  "temperature": 1.0,
  "text": {
    "format": {
      "type": "text"
    }
  },
  "tool_choice": "auto",
  "tools": [
    {
      "type": "function",
      "description": "Get the current weather in a given location",
      "name": "get_current_weather",
      "parameters": {
        "type": "object",
        "properties": {
          "location": {
            "type": "string",
            "description": "The city and state, e.g. San Francisco, CA"
          },
          "unit": {
            "type": "string",
            "enum": [
              "celsius",
              "fahrenheit"
            ]
          }
        },
        "required": [
          "location",
          "unit"
        ]
      },
      "strict": true
    }
  ],
  "top_p": 1.0,
  "truncation": "disabled",
  "usage": {
    "input_tokens": 291,
    "output_tokens": 23,
    "output_tokens_details": {
      "reasoning_tokens": 0
    },
    "total_tokens": 314
  },
  "user": null,
  "metadata": {}
}
```
### Reasoning
#### Request (curl)
```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "o3-mini",
    "input": "How much wood would a woodchuck chuck?",
    "reasoning": {
      "effort": "high"
    }
  }'
```
#### Request (javascript)
```javascript
import OpenAI from "openai";
const openai = new OpenAI();

const response = await openai.responses.create({
    model: "o3-mini",
    input: "How much wood would a woodchuck chuck?",
    reasoning: {
      effort: "high"
    }
});

console.log(response);
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="o3-mini",
    input="How much wood would a woodchuck chuck?",
    reasoning={
        "effort": "high"
    }
)

print(response)
```
#### Request (csharp)
```csharp
using System;
using OpenAI.Responses;

OpenAIResponseClient client = new(
    model: "o3-mini",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

string userInputText = "How much wood would a woodchuck chuck?";

ResponseCreationOptions options = new()
{
    ReasoningOptions = new()
    {
        ReasoningEffortLevel = ResponseReasoningEffortLevel.High,
    },
};

OpenAIResponse response = client.CreateResponse(userInputText, options);

Console.WriteLine(response.GetOutputText());
```
#### Response
```json
{
  "id": "resp_67ccd7eca01881908ff0b5146584e408072912b2993db808",
  "object": "response",
  "created_at": 1741477868,
  "status": "completed",
  "completed_at": 1741477869,
  "error": null,
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "model": "o1-2024-12-17",
  "output": [
    {
      "type": "message",
      "id": "msg_67ccd7f7b5848190a6f3e95d809f6b44072912b2993db808",
      "status": "completed",
      "role": "assistant",
      "content": [
        {
          "type": "output_text",
          "text": "The classic tongue twister...",
          "annotations": []
        }
      ]
    }
  ],
  "parallel_tool_calls": true,
  "previous_response_id": null,
  "reasoning": {
    "effort": "high",
    "summary": null
  },
  "store": true,
  "temperature": 1.0,
  "text": {
    "format": {
      "type": "text"
    }
  },
  "tool_choice": "auto",
  "tools": [],
  "top_p": 1.0,
  "truncation": "disabled",
  "usage": {
    "input_tokens": 81,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens": 1035,
    "output_tokens_details": {
      "reasoning_tokens": 832
    },
    "total_tokens": 1116
  },
  "user": null,
  "metadata": {}
}
```
