# Create chat completion

Source: https://platform.openai.com/docs/api-reference/chat/create

`POST /v1/chat/completions`

**Starting a new project?** We recommend trying [Responses](../responses/index.md) 
to take advantage of the latest OpenAI platform features. Compare
[Chat Completions with Responses](https://platform.openai.com/docs/guides/responses-vs-chat-completions?api-mode=responses).

---

Creates a model response for the given chat conversation. Learn more in the
[text generation](https://platform.openai.com/docs/guides/text-generation), [vision](https://platform.openai.com/docs/guides/vision),
and [audio](https://platform.openai.com/docs/guides/audio) guides.

Parameter support can differ depending on the model used to generate the
response, particularly for newer reasoning models. Parameters that are only
supported for reasoning models are noted below. For the current state of 
unsupported parameters in reasoning models, 
[refer to the reasoning guide](https://platform.openai.com/docs/guides/reasoning).

## Request body
### application/json
- `metadata` (object | null, optional)
- `top_logprobs` (integer, optional): An integer between 0 and 20 specifying the number of most likely tokens to
  return at each token position, each with an associated log probability.
  `logprobs` must be set to `true` if this parameter is used.
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
- `messages` (array<object>, required): A list of messages comprising the conversation so far. Depending on the
  [model](https://platform.openai.com/docs/models) you use, different message types (modalities) are
  supported, like [text](https://platform.openai.com/docs/guides/text-generation),
  [images](https://platform.openai.com/docs/guides/vision), and [audio](https://platform.openai.com/docs/guides/audio).
- `model` (string, required): Model ID used to generate the response, like `gpt-4o` or `o3`. OpenAI
  offers a wide range of models with different capabilities, performance
  characteristics, and price points. Refer to the [model guide](https://platform.openai.com/docs/models)
  to browse and compare available models.
- `modalities` (array<string> | null, optional)
- `verbosity` (string | null, optional)
- `reasoning_effort` (string | null, optional)
- `max_completion_tokens` (integer, optional): An upper bound for the number of tokens that can be generated for a completion, including visible output tokens and [reasoning tokens](https://platform.openai.com/docs/guides/reasoning).
- `frequency_penalty` (number, optional): Number between -2.0 and 2.0. Positive values penalize new tokens based on
  their existing frequency in the text so far, decreasing the model's
  likelihood to repeat the same line verbatim. Default: `0`.
- `presence_penalty` (number, optional): Number between -2.0 and 2.0. Positive values penalize new tokens based on
  whether they appear in the text so far, increasing the model's likelihood
  to talk about new topics. Default: `0`.
- `web_search_options` (object, optional): This tool searches the web for relevant results to use in a response.
  Learn more about the [web search tool](https://platform.openai.com/docs/guides/tools-web-search?api-mode=chat).
  - `user_location` (object, optional): Approximate location parameters for the search.
    - `type` (string, required): The type of location approximation. Always `approximate`. Enum: 'approximate'.
    - `approximate` (object, required): Approximate location parameters for the search.
      - `country` (string, optional): The two-letter 
        [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1) of the user,
        e.g. `US`.
      - `region` (string, optional): Free text input for the region of the user, e.g. `California`.
      - `city` (string, optional): Free text input for the city of the user, e.g. `San Francisco`.
      - `timezone` (string, optional): The [IANA timezone](https://timeapi.io/documentation/iana-timezones) 
        of the user, e.g. `America/Los_Angeles`.
  - `search_context_size` (string, optional): High level guidance for the amount of context window space to use for the 
    search. One of `low`, `medium`, or `high`. `medium` is the default. Enum: 'low', 'medium', 'high'. Default: `medium`.
- `response_format` (object, optional): An object specifying the format that the model must output.
  
  Setting to `{ "type": "json_schema", "json_schema": {...} }` enables
  Structured Outputs which ensures the model will match your supplied JSON
  schema. Learn more in the [Structured Outputs
  guide](https://platform.openai.com/docs/guides/structured-outputs).
  
  Setting to `{ "type": "json_object" }` enables the older JSON mode, which
  ensures the message the model generates is valid JSON. Using `json_schema`
  is preferred for models that support it.
  - Variant (object):
    - `type` (string, required): The type of response format being defined. Always `text`. Enum: 'text'.
  - Variant (object):
    - `type` (string, required): The type of response format being defined. Always `json_schema`. Enum: 'json_schema'.
    - `json_schema` (object, required): Structured Outputs configuration options, including a JSON Schema.
      - `description` (string, optional): A description of what the response format is for, used by the model to
        determine how to respond in the format.
      - `name` (string, required): The name of the response format. Must be a-z, A-Z, 0-9, or contain
        underscores and dashes, with a maximum length of 64.
      - `schema` (object, optional): The schema for the response format, described as a JSON Schema object.
        Learn how to build JSON schemas [here](https://json-schema.org/).
      - `strict` (boolean | null, optional)
  - Variant (object):
    - `type` (string, required): The type of response format being defined. Always `json_object`. Enum: 'json_object'.
- `audio` (object, optional): Parameters for audio output. Required when audio output is requested with
  `modalities: ["audio"]`. [Learn more](https://platform.openai.com/docs/guides/audio).
  - `voice` (string | object, required): The voice the model uses to respond. Supported built-in voices are
    `alloy`, `ash`, `ballad`, `coral`, `echo`, `fable`, `nova`, `onyx`,
    `sage`, `shimmer`, `marin`, and `cedar`. You may also provide a
    custom voice object with an `id`, for example `{ "id": "voice_1234" }`.
    - Variant (object):
      - `id` (string, required): The custom voice ID, e.g. `voice_1234`.
  - `format` (string, required): Specifies the output audio format. Must be one of `wav`, `mp3`, `flac`,
    `opus`, or `pcm16`. Enum: 'wav', 'aac', 'mp3', 'flac', 'opus', 'pcm16'.
- `store` (boolean, optional): Whether or not to store the output of this chat completion request for
  use in our [model distillation](https://platform.openai.com/docs/guides/distillation) or
  [evals](https://platform.openai.com/docs/guides/evals) products.
  
  Supports text and image inputs. Note: image inputs over 8MB will be dropped. Default: `False`.
- `stream` (boolean, optional): If set to true, the model response data will be streamed to the client
  as it is generated using [server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events#Event_stream_format).
  See the [Streaming section below](../chat-streaming/index.md)
  for more information, along with the [streaming responses](https://platform.openai.com/docs/guides/streaming-responses)
  guide for more information on how to handle the streaming events. Default: `False`.
- `stop` (string | array<string>, optional): Not supported with latest reasoning models `o3` and `o4-mini`.
  
  Up to 4 sequences where the API will stop generating further tokens. The
  returned text will not contain the stop sequence.
- `logit_bias` (object, optional): Modify the likelihood of specified tokens appearing in the completion.
  
  Accepts a JSON object that maps tokens (specified by their token ID in the
  tokenizer) to an associated bias value from -100 to 100. Mathematically,
  the bias is added to the logits generated by the model prior to sampling.
  The exact effect will vary per model, but values between -1 and 1 should
  decrease or increase likelihood of selection; values like -100 or 100
  should result in a ban or exclusive selection of the relevant token.
- `logprobs` (boolean, optional): Whether to return log probabilities of the output tokens or not. If true,
  returns the log probabilities of each output token returned in the
  `content` of `message`. Default: `False`.
- `max_tokens` (integer, optional): The maximum number of [tokens](https://platform.openai.com/tokenizer) that can be generated in the
  chat completion. This value can be used to control
  [costs](https://openai.com/api/pricing/) for text generated via API.
  
  This value is now deprecated in favor of `max_completion_tokens`, and is
  not compatible with [o-series models](https://platform.openai.com/docs/guides/reasoning). Deprecated.
- `n` (integer, optional): How many chat completion choices to generate for each input message. Note that you will be charged based on the number of generated tokens across all of the choices. Keep `n` as `1` to minimize costs. Default: `1`.
- `prediction` (object, optional): Configuration for a [Predicted Output](https://platform.openai.com/docs/guides/predicted-outputs),
  which can greatly improve response times when large parts of the model
  response are known ahead of time. This is most common when you are
  regenerating a file with only minor changes to most of the content.
  - Variant (object):
    - `type` (string, required): The type of the predicted content you want to provide. This type is
      currently always `content`. Enum: 'content'.
    - `content` (string | array<object>, required): The content that should be matched when generating a model response.
      If generated tokens would match this content, the entire model response
      can be returned much more quickly.
- `seed` (integer, optional): This feature is in Beta.
  If specified, our system will make a best effort to sample deterministically, such that repeated requests with the same `seed` and parameters should return the same result.
  Determinism is not guaranteed, and you should refer to the `system_fingerprint` response parameter to monitor changes in the backend. Deprecated.
- `stream_options` (object | null, optional)
  - Variant (object):
    - `include_usage` (boolean, optional): If set, an additional chunk will be streamed before the `data: [DONE]`
      message. The `usage` field on this chunk shows the token usage statistics
      for the entire request, and the `choices` field will always be an empty
      array.
      
      All other chunks will also include a `usage` field, but with a null
      value. **NOTE:** If the stream is interrupted, you may not receive the
      final usage chunk which contains the total token usage for the request.
    - `include_obfuscation` (boolean, optional): When true, stream obfuscation will be enabled. Stream obfuscation adds
      random characters to an `obfuscation` field on streaming delta events to
      normalize payload sizes as a mitigation to certain side-channel attacks.
      These obfuscation fields are included by default, but add a small amount
      of overhead to the data stream. You can set `include_obfuscation` to
      false to optimize for bandwidth if you trust the network links between
      your application and the OpenAI API.
- `tools` (array<object>, optional): A list of tools the model may call. You can provide either
  [custom tools](https://platform.openai.com/docs/guides/function-calling#custom-tools) or
  [function tools](https://platform.openai.com/docs/guides/function-calling).
- `tool_choice` (string | object, optional): Controls which (if any) tool is called by the model.
  `none` means the model will not call any tool and instead generates a message.
  `auto` means the model can pick between generating a message or calling one or more tools.
  `required` means the model must call one or more tools.
  Specifying a particular tool via `{"type": "function", "function": {"name": "my_function"}}` forces the model to call that tool.
  
  `none` is the default when no tools are present. `auto` is the default if tools are present.
  - Variant (object):
    - `type` (string, required): Allowed tool configuration type. Always `allowed_tools`. Enum: 'allowed_tools'.
    - `allowed_tools` (object, required): Constrains the tools available to the model to a pre-defined set.
      - `mode` (string, required): Constrains the tools available to the model to a pre-defined set.
        
        `auto` allows the model to pick from among the allowed tools and generate a
        message.
        
        `required` requires the model to call one or more of the allowed tools. Enum: 'auto', 'required'.
      - `tools` (array<object>, required): A list of tool definitions that the model should be allowed to call.
        
        For the Chat Completions API, the list of tool definitions might look like:
        ```json
        [
          { "type": "function", "function": { "name": "get_weather" } },
          { "type": "function", "function": { "name": "get_time" } }
        ]
        ```
  - Variant (object):
    - `type` (string, required): For function calling, the type is always `function`. Enum: 'function'.
    - `function` (object, required)
      - `name` (string, required): The name of the function to call.
  - Variant (object):
    - `type` (string, required): For custom tool calling, the type is always `custom`. Enum: 'custom'.
    - `custom` (object, required)
      - `name` (string, required): The name of the custom tool to call.
- `parallel_tool_calls` (boolean, optional): Whether to enable [parallel function calling](https://platform.openai.com/docs/guides/function-calling#configuring-parallel-function-calling) during tool use. Default: `True`.
- `function_call` (string | object, optional): Deprecated in favor of `tool_choice`.
  
  Controls which (if any) function is called by the model.
  
  `none` means the model will not call a function and instead generates a
  message.
  
  `auto` means the model can pick between generating a message or calling a
  function.
  
  Specifying a particular function via `{"name": "my_function"}` forces the
  model to call that function.
  
  `none` is the default when no functions are present. `auto` is the default
  if functions are present. Deprecated.
  - Variant (object):
    - `name` (string, required): The name of the function to call.
- `functions` (array<object>, optional): Deprecated in favor of `tools`.
  
  A list of functions the model may generate JSON inputs for. Deprecated.
  - Items:
    - `description` (string, optional): A description of what the function does, used by the model to choose when and how to call the function.
    - `name` (string, required): The name of the function to be called. Must be a-z, A-Z, 0-9, or contain underscores and dashes, with a maximum length of 64.
    - `parameters` (object, optional): The parameters the functions accepts, described as a JSON Schema object. See the [guide](https://platform.openai.com/docs/guides/function-calling) for examples, and the [JSON Schema reference](https://json-schema.org/understanding-json-schema/) for documentation about the format. 
      
      Omitting `parameters` defines a function with an empty parameter list.

## Responses
### 200
OK
#### application/json
- `id` (string, required): A unique identifier for the chat completion.
- `choices` (array<object>, required): A list of chat completion choices. Can be more than one if `n` is greater than 1.
  - Items:
    - `finish_reason` (string, required): The reason the model stopped generating tokens. This will be `stop` if the model hit a natural stop point or a provided stop sequence,
      `length` if the maximum number of tokens specified in the request was reached,
      `content_filter` if content was omitted due to a flag from our content filters,
      `tool_calls` if the model called a tool, or `function_call` (deprecated) if the model called a function. Enum: 'stop', 'length', 'tool_calls', 'content_filter', 'function_call'.
    - `index` (integer, required): The index of the choice in the list of choices.
    - `message` (object, required): A chat completion message generated by the model.
      - `content` (string | null, required)
      - `refusal` (string | null, required)
      - `tool_calls` (array<object>, optional): The tool calls generated by the model, such as function calls.
      - `annotations` (array<object>, optional): Annotations for the message, when applicable, as when using the
        [web search tool](https://platform.openai.com/docs/guides/tools-web-search?api-mode=chat).
        - Items:
          - ...
      - `role` (string, required): The role of the author of this message. Enum: 'assistant'.
      - `function_call` (object, optional): Deprecated and replaced by `tool_calls`. The name and arguments of a function that should be called, as generated by the model. Deprecated.
        - `arguments` (string, required): The arguments to call the function with, as generated by the model in JSON format. Note that the model does not always generate valid JSON, and may hallucinate parameters not defined by your function schema. Validate the arguments in your code before calling your function.
        - `name` (string, required): The name of the function to call.
      - `audio` (object | null, optional)
        - Variant (object):
          - ...
    - `logprobs` (object | null, required)
      - Variant (object):
        - `content` (array<object> | null, required)
        - `refusal` (array<object> | null, required)
- `created` (integer, required): The Unix timestamp (in seconds) of when the chat completion was created.
- `model` (string, required): The model used for the chat completion.
- `service_tier` (string | null, optional)
- `system_fingerprint` (string, optional): This fingerprint represents the backend configuration that the model runs with.
  
  Can be used in conjunction with the `seed` request parameter to understand when backend changes have been made that might impact determinism. Deprecated.
- `object` (string, required): The object type, which is always `chat.completion`. Enum: 'chat.completion'.
- `usage` (object, optional): Usage statistics for the completion request.
  - `completion_tokens` (integer, required): Number of tokens in the generated completion. Default: `0`.
  - `prompt_tokens` (integer, required): Number of tokens in the prompt. Default: `0`.
  - `total_tokens` (integer, required): Total number of tokens used in the request (prompt + completion). Default: `0`.
  - `completion_tokens_details` (object, optional): Breakdown of tokens used in a completion.
    - `accepted_prediction_tokens` (integer, optional): When using Predicted Outputs, the number of tokens in the
      prediction that appeared in the completion. Default: `0`.
    - `audio_tokens` (integer, optional): Audio input tokens generated by the model. Default: `0`.
    - `reasoning_tokens` (integer, optional): Tokens generated by the model for reasoning. Default: `0`.
    - `rejected_prediction_tokens` (integer, optional): When using Predicted Outputs, the number of tokens in the
      prediction that did not appear in the completion. However, like
      reasoning tokens, these tokens are still counted in the total
      completion tokens for purposes of billing, output, and context window
      limits. Default: `0`.
  - `prompt_tokens_details` (object, optional): Breakdown of tokens used in the prompt.
    - `audio_tokens` (integer, optional): Audio input tokens present in the prompt. Default: `0`.
    - `cached_tokens` (integer, optional): Cached tokens present in the prompt. Default: `0`.
#### text/event-stream
- `id` (string, required): A unique identifier for the chat completion. Each chunk has the same ID.
- `choices` (array<object>, required): A list of chat completion choices. Can contain more than one elements if `n` is greater than 1. Can also be empty for the
  last chunk if you set `stream_options: {"include_usage": true}`.
  - Items:
    - `delta` (object, required): A chat completion delta generated by streamed model responses.
      - `content` (string | null, optional)
      - `function_call` (object, optional): Deprecated and replaced by `tool_calls`. The name and arguments of a function that should be called, as generated by the model. Deprecated.
        - `arguments` (string, optional): The arguments to call the function with, as generated by the model in JSON format. Note that the model does not always generate valid JSON, and may hallucinate parameters not defined by your function schema. Validate the arguments in your code before calling your function.
        - `name` (string, optional): The name of the function to call.
      - `tool_calls` (array<object>, optional)
        - Items:
          - ...
      - `role` (string, optional): The role of the author of this message. Enum: 'developer', 'system', 'user', 'assistant', 'tool'.
      - `refusal` (string | null, optional)
    - `logprobs` (object, optional): Log probability information for the choice.
      - `content` (array<object>, required): A list of message content tokens with log probability information.
        - Items:
          - ...
      - `refusal` (array<object>, required): A list of message refusal tokens with log probability information.
        - Items:
          - ...
    - `finish_reason` (string, required): The reason the model stopped generating tokens. This will be `stop` if the model hit a natural stop point or a provided stop sequence,
      `length` if the maximum number of tokens specified in the request was reached,
      `content_filter` if content was omitted due to a flag from our content filters,
      `tool_calls` if the model called a tool, or `function_call` (deprecated) if the model called a function. Enum: 'stop', 'length', 'tool_calls', 'content_filter', 'function_call'.
    - `index` (integer, required): The index of the choice in the list of choices.
- `created` (integer, required): The Unix timestamp (in seconds) of when the chat completion was created. Each chunk has the same timestamp.
- `model` (string, required): The model to generate the completion.
- `service_tier` (string | null, optional)
- `system_fingerprint` (string, optional): This fingerprint represents the backend configuration that the model runs with.
  Can be used in conjunction with the `seed` request parameter to understand when backend changes have been made that might impact determinism. Deprecated.
- `object` (string, required): The object type, which is always `chat.completion.chunk`. Enum: 'chat.completion.chunk'.
- `usage` (object, optional): Usage statistics for the completion request.
  - `completion_tokens` (integer, required): Number of tokens in the generated completion. Default: `0`.
  - `prompt_tokens` (integer, required): Number of tokens in the prompt. Default: `0`.
  - `total_tokens` (integer, required): Total number of tokens used in the request (prompt + completion). Default: `0`.
  - `completion_tokens_details` (object, optional): Breakdown of tokens used in a completion.
    - `accepted_prediction_tokens` (integer, optional): When using Predicted Outputs, the number of tokens in the
      prediction that appeared in the completion. Default: `0`.
    - `audio_tokens` (integer, optional): Audio input tokens generated by the model. Default: `0`.
    - `reasoning_tokens` (integer, optional): Tokens generated by the model for reasoning. Default: `0`.
    - `rejected_prediction_tokens` (integer, optional): When using Predicted Outputs, the number of tokens in the
      prediction that did not appear in the completion. However, like
      reasoning tokens, these tokens are still counted in the total
      completion tokens for purposes of billing, output, and context window
      limits. Default: `0`.
  - `prompt_tokens_details` (object, optional): Breakdown of tokens used in the prompt.
    - `audio_tokens` (integer, optional): Audio input tokens present in the prompt. Default: `0`.
    - `cached_tokens` (integer, optional): Cached tokens present in the prompt. Default: `0`.

## Returns
Returns a [chat completion](object.md) object, or a streamed sequence of [chat completion chunk](../chat-streaming/index.md) objects if the request is streamed.

## Examples
### Default
#### Request (curl)
```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "VAR_chat_model_id",
    "messages": [
      {
        "role": "developer",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "Hello!"
      }
    ]
  }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

completion = client.chat.completions.create(
  model="VAR_chat_model_id",
  messages=[
    {"role": "developer", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello!"}
  ]
)

print(completion.choices[0].message)
```
#### Request (csharp)
```csharp
using System;
using System.Collections.Generic;

using OpenAI.Chat;

ChatClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

List<ChatMessage> messages =
[
    new SystemChatMessage("You are a helpful assistant."),
    new UserChatMessage("Hello!")
];

ChatCompletion completion = client.CompleteChat(messages);

Console.WriteLine(completion.Content[0].Text);
```
#### Response
```json
{
  "id": "chatcmpl-B9MBs8CjcvOU2jLn4n570S5qMJKcT",
  "object": "chat.completion",
  "created": 1741569952,
  "model": "gpt-4.1-2025-04-14",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! How can I assist you today?",
        "refusal": null,
        "annotations": []
      },
      "logprobs": null,
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 19,
    "completion_tokens": 10,
    "total_tokens": 29,
    "prompt_tokens_details": {
      "cached_tokens": 0,
      "audio_tokens": 0
    },
    "completion_tokens_details": {
      "reasoning_tokens": 0,
      "audio_tokens": 0,
      "accepted_prediction_tokens": 0,
      "rejected_prediction_tokens": 0
    }
  },
  "service_tier": "default"
}
```
### Image input
#### Request (curl)
```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4.1",
    "messages": [
      {
        "role": "user",
        "content": [
          {
            "type": "text",
            "text": "What is in this image?"
          },
          {
            "type": "image_url",
            "image_url": {
              "url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg"
            }
          }
        ]
      }
    ],
    "max_tokens": 300
  }'
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

response = client.chat.completions.create(
    model="gpt-4.1",
    messages=[
        {
            "role": "user",
            "content": [
                {"type": "text", "text": "What's in this image?"},
                {
                    "type": "image_url",
                    "image_url": {
                        "url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
                    }
                },
            ],
        }
    ],
    max_tokens=300,
)

print(response.choices[0])
```
#### Request (csharp)
```csharp
using System;
using System.Collections.Generic;

using OpenAI.Chat;

ChatClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

List<ChatMessage> messages =
[
    new UserChatMessage(
    [
        ChatMessageContentPart.CreateTextPart("What's in this image?"),
        ChatMessageContentPart.CreateImagePart(new Uri("https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg"))
    ])
];

ChatCompletion completion = client.CompleteChat(messages);

Console.WriteLine(completion.Content[0].Text);
```
#### Response
```json
{
  "id": "chatcmpl-B9MHDbslfkBeAs8l4bebGdFOJ6PeG",
  "object": "chat.completion",
  "created": 1741570283,
  "model": "gpt-4.1-2025-04-14",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "The image shows a wooden boardwalk path running through a lush green field or meadow. The sky is bright blue with some scattered clouds, giving the scene a serene and peaceful atmosphere. Trees and shrubs are visible in the background.",
        "refusal": null,
        "annotations": []
      },
      "logprobs": null,
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 1117,
    "completion_tokens": 46,
    "total_tokens": 1163,
    "prompt_tokens_details": {
      "cached_tokens": 0,
      "audio_tokens": 0
    },
    "completion_tokens_details": {
      "reasoning_tokens": 0,
      "audio_tokens": 0,
      "accepted_prediction_tokens": 0,
      "rejected_prediction_tokens": 0
    }
  },
  "service_tier": "default"
}
```
### Streaming
#### Request (curl)
```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "VAR_chat_model_id",
    "messages": [
      {
        "role": "developer",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "Hello!"
      }
    ],
    "stream": true
  }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

completion = client.chat.completions.create(
  model="VAR_chat_model_id",
  messages=[
    {"role": "developer", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello!"}
  ],
  stream=True
)

for chunk in completion:
  print(chunk.choices[0].delta)
```
#### Request (csharp)
```csharp
using System;
using System.ClientModel;
using System.Collections.Generic;
using System.Threading.Tasks;

using OpenAI.Chat;

ChatClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

List<ChatMessage> messages =
[
    new SystemChatMessage("You are a helpful assistant."),
    new UserChatMessage("Hello!")
];

AsyncCollectionResult<StreamingChatCompletionUpdate> completionUpdates = client.CompleteChatStreamingAsync(messages);

await foreach (StreamingChatCompletionUpdate completionUpdate in completionUpdates)
{
    if (completionUpdate.ContentUpdate.Count > 0)
    {
        Console.Write(completionUpdate.ContentUpdate[0].Text);
    }
}
```
#### Response
```json
{"id":"chatcmpl-123","object":"chat.completion.chunk","created":1694268190,"model":"gpt-4o-mini", "system_fingerprint": "fp_44709d6fcb", "choices":[{"index":0,"delta":{"role":"assistant","content":""},"logprobs":null,"finish_reason":null}]}

{"id":"chatcmpl-123","object":"chat.completion.chunk","created":1694268190,"model":"gpt-4o-mini", "system_fingerprint": "fp_44709d6fcb", "choices":[{"index":0,"delta":{"content":"Hello"},"logprobs":null,"finish_reason":null}]}

....

{"id":"chatcmpl-123","object":"chat.completion.chunk","created":1694268190,"model":"gpt-4o-mini", "system_fingerprint": "fp_44709d6fcb", "choices":[{"index":0,"delta":{},"logprobs":null,"finish_reason":"stop"}]}
```
### Functions
#### Request (curl)
```bash
curl https://api.openai.com/v1/chat/completions \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $OPENAI_API_KEY" \
-d '{
  "model": "gpt-4.1",
  "messages": [
    {
      "role": "user",
      "content": "What is the weather like in Boston today?"
    }
  ],
  "tools": [
    {
      "type": "function",
      "function": {
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
          "required": ["location"]
        }
      }
    }
  ],
  "tool_choice": "auto"
}'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

tools = [
  {
    "type": "function",
    "function": {
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
        "required": ["location"],
      },
    }
  }
]
messages = [{"role": "user", "content": "What's the weather like in Boston today?"}]
completion = client.chat.completions.create(
  model="VAR_chat_model_id",
  messages=messages,
  tools=tools,
  tool_choice="auto"
)

print(completion)
```
#### Request (csharp)
```csharp
using System;
using System.Collections.Generic;

using OpenAI.Chat;

ChatClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

ChatTool getCurrentWeatherTool = ChatTool.CreateFunctionTool(
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
                "unit": {
                    "type": "string",
                    "enum": [ "celsius", "fahrenheit" ]
                }
            },
            "required": [ "location" ]
        }
    """)
);

List<ChatMessage> messages =
[
    new UserChatMessage("What's the weather like in Boston today?"),
];

ChatCompletionOptions options = new()
{
    Tools =
    {
        getCurrentWeatherTool
    },
    ToolChoice = ChatToolChoice.CreateAutoChoice(),
};

ChatCompletion completion = client.CompleteChat(messages, options);
```
#### Response
```json
{
  "id": "chatcmpl-abc123",
  "object": "chat.completion",
  "created": 1699896916,
  "model": "gpt-4o-mini",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": null,
        "tool_calls": [
          {
            "id": "call_abc123",
            "type": "function",
            "function": {
              "name": "get_current_weather",
              "arguments": "{\n\"location\": \"Boston, MA\"\n}"
            }
          }
        ]
      },
      "logprobs": null,
      "finish_reason": "tool_calls"
    }
  ],
  "usage": {
    "prompt_tokens": 82,
    "completion_tokens": 17,
    "total_tokens": 99,
    "completion_tokens_details": {
      "reasoning_tokens": 0,
      "accepted_prediction_tokens": 0,
      "rejected_prediction_tokens": 0
    }
  }
}
```
### Logprobs
#### Request (curl)
```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "VAR_chat_model_id",
    "messages": [
      {
        "role": "user",
        "content": "Hello!"
      }
    ],
    "logprobs": true,
    "top_logprobs": 2
  }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

completion = client.chat.completions.create(
  model="VAR_chat_model_id",
  messages=[
    {"role": "user", "content": "Hello!"}
  ],
  logprobs=True,
  top_logprobs=2
)

print(completion.choices[0].message)
print(completion.choices[0].logprobs)
```
#### Request (csharp)
```csharp
using System;
using System.Collections.Generic;

using OpenAI.Chat;

ChatClient client = new(
    model: "gpt-4.1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

List<ChatMessage> messages =
[
    new UserChatMessage("Hello!")
];

ChatCompletionOptions options = new()
{
    IncludeLogProbabilities = true,
    TopLogProbabilityCount = 2
};

ChatCompletion completion = client.CompleteChat(messages, options);

Console.WriteLine(completion.Content[0].Text);
```
#### Response
```json
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1702685778,
  "model": "gpt-4o-mini",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! How can I assist you today?"
      },
      "logprobs": {
        "content": [
          {
            "token": "Hello",
            "logprob": -0.31725305,
            "bytes": [72, 101, 108, 108, 111],
            "top_logprobs": [
              {
                "token": "Hello",
                "logprob": -0.31725305,
                "bytes": [72, 101, 108, 108, 111]
              },
              {
                "token": "Hi",
                "logprob": -1.3190403,
                "bytes": [72, 105]
              }
            ]
          },
          {
            "token": "!",
            "logprob": -0.02380986,
            "bytes": [
              33
            ],
            "top_logprobs": [
              {
                "token": "!",
                "logprob": -0.02380986,
                "bytes": [33]
              },
              {
                "token": " there",
                "logprob": -3.787621,
                "bytes": [32, 116, 104, 101, 114, 101]
              }
            ]
          },
          {
            "token": " How",
            "logprob": -0.000054669687,
            "bytes": [32, 72, 111, 119],
            "top_logprobs": [
              {
                "token": " How",
                "logprob": -0.000054669687,
                "bytes": [32, 72, 111, 119]
              },
              {
                "token": "<|end|>",
                "logprob": -10.953937,
                "bytes": null
              }
            ]
          },
          {
            "token": " can",
            "logprob": -0.015801601,
            "bytes": [32, 99, 97, 110],
            "top_logprobs": [
              {
                "token": " can",
                "logprob": -0.015801601,
                "bytes": [32, 99, 97, 110]
              },
              {
                "token": " may",
                "logprob": -4.161023,
                "bytes": [32, 109, 97, 121]
              }
            ]
          },
          {
            "token": " I",
            "logprob": -3.7697225e-6,
            "bytes": [
              32,
              73
            ],
            "top_logprobs": [
              {
                "token": " I",
                "logprob": -3.7697225e-6,
                "bytes": [32, 73]
              },
              {
                "token": " assist",
                "logprob": -13.596657,
                "bytes": [32, 97, 115, 115, 105, 115, 116]
              }
            ]
          },
          {
            "token": " assist",
            "logprob": -0.04571125,
            "bytes": [32, 97, 115, 115, 105, 115, 116],
            "top_logprobs": [
              {
                "token": " assist",
                "logprob": -0.04571125,
                "bytes": [32, 97, 115, 115, 105, 115, 116]
              },
              {
                "token": " help",
                "logprob": -3.1089056,
                "bytes": [32, 104, 101, 108, 112]
              }
            ]
          },
          {
            "token": " you",
            "logprob": -5.4385737e-6,
            "bytes": [32, 121, 111, 117],
            "top_logprobs": [
              {
                "token": " you",
                "logprob": -5.4385737e-6,
                "bytes": [32, 121, 111, 117]
              },
              {
                "token": " today",
                "logprob": -12.807695,
                "bytes": [32, 116, 111, 100, 97, 121]
              }
            ]
          },
          {
            "token": " today",
            "logprob": -0.0040071653,
            "bytes": [32, 116, 111, 100, 97, 121],
            "top_logprobs": [
              {
                "token": " today",
                "logprob": -0.0040071653,
                "bytes": [32, 116, 111, 100, 97, 121]
              },
              {
                "token": "?",
                "logprob": -5.5247097,
                "bytes": [63]
              }
            ]
          },
          {
            "token": "?",
            "logprob": -0.0008108172,
            "bytes": [63],
            "top_logprobs": [
              {
                "token": "?",
                "logprob": -0.0008108172,
                "bytes": [63]
              },
              {
                "token": "?\n",
                "logprob": -7.184561,
                "bytes": [63, 10]
              }
            ]
          }
        ]
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 9,
    "completion_tokens": 9,
    "total_tokens": 18,
    "completion_tokens_details": {
      "reasoning_tokens": 0,
      "accepted_prediction_tokens": 0,
      "rejected_prediction_tokens": 0
    }
  },
  "system_fingerprint": null
}
```
