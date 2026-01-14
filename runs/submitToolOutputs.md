# Submit tool outputs to run

Source: https://platform.openai.com/docs/api-reference/runs/submitToolOutputs

`POST /v1/threads/{thread_id}/runs/{run_id}/submit_tool_outputs`

When a run has the `status: "requires_action"` and `required_action.type` is `submit_tool_outputs`, this endpoint can be used to submit the outputs from the tool calls once they're all completed. All outputs must be submitted in a single request.

## Parameters
- `thread_id` (path, string, required): The ID of the [thread](../threads/index.md) to which this run belongs.
- `run_id` (path, string, required): The ID of the run that requires the tool output submission.

## Request body
### application/json
- `tool_outputs` (array<object>, required): A list of tools for which the outputs are being submitted.
  - Items:
    - `tool_call_id` (string, optional): The ID of the tool call in the `required_action` object within the run object the output is being submitted for.
    - `output` (string, optional): The output of the tool call to be submitted to continue the run.
- `stream` (boolean | null, optional)

## Responses
### 200
OK
#### application/json
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `thread.run`. Enum: 'thread.run'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the run was created.
- `thread_id` (string, required): The ID of the [thread](../threads/index.md) that was executed on as a part of this run.
- `assistant_id` (string, required): The ID of the [assistant](../assistants/index.md) used for execution of this run.
- `status` (string, required): The status of the run, which can be either `queued`, `in_progress`, `requires_action`, `cancelling`, `cancelled`, `failed`, `completed`, `incomplete`, or `expired`. Enum: 'queued', 'in_progress', 'requires_action', 'cancelling', 'cancelled', 'failed', 'completed', 'incomplete', 'expired'.
- `required_action` (object, required): Details on the action required to continue the run. Will be `null` if no action is required.
  - `type` (string, required): For now, this is always `submit_tool_outputs`. Enum: 'submit_tool_outputs'.
  - `submit_tool_outputs` (object, required): Details on the tool outputs needed for this run to continue.
    - `tool_calls` (array<object>, required): A list of the relevant tool calls.
      - Items:
        - `id` (string, required): The ID of the tool call. This ID must be referenced when you submit the tool outputs in using the [Submit tool outputs to run](submitToolOutputs.md) endpoint.
        - `type` (string, required): The type of tool call the output is required for. For now, this is always `function`. Enum: 'function'.
        - `function` (object, required): The function definition.
          - ...
- `last_error` (object, required): The last error associated with this run. Will be `null` if there are no errors.
  - `code` (string, required): One of `server_error`, `rate_limit_exceeded`, or `invalid_prompt`. Enum: 'server_error', 'rate_limit_exceeded', 'invalid_prompt'.
  - `message` (string, required): A human-readable description of the error.
- `expires_at` (integer, required): The Unix timestamp (in seconds) for when the run will expire.
- `started_at` (integer, required): The Unix timestamp (in seconds) for when the run was started.
- `cancelled_at` (integer, required): The Unix timestamp (in seconds) for when the run was cancelled.
- `failed_at` (integer, required): The Unix timestamp (in seconds) for when the run failed.
- `completed_at` (integer, required): The Unix timestamp (in seconds) for when the run was completed.
- `incomplete_details` (object, required): Details on why the run is incomplete. Will be `null` if the run is not incomplete.
  - `reason` (string, optional): The reason why the run is incomplete. This will point to which specific token limit was reached over the course of the run. Enum: 'max_completion_tokens', 'max_prompt_tokens'.
- `model` (string, required): The model that the [assistant](../assistants/index.md) used for this run.
- `instructions` (string, required): The instructions that the [assistant](../assistants/index.md) used for this run.
- `tools` (array<object>, required): The list of tools that the [assistant](../assistants/index.md) used for this run. Default: `[]`.
- `metadata` (object | null, required)
- `usage` (object | null, required)
  - Variant (object):
    - `completion_tokens` (integer, required): Number of completion tokens used over the course of the run.
    - `prompt_tokens` (integer, required): Number of prompt tokens used over the course of the run.
    - `total_tokens` (integer, required): Total number of tokens used (prompt + completion).
- `temperature` (number, optional): The sampling temperature used for this run. If not set, defaults to 1.
- `top_p` (number, optional): The nucleus sampling value used for this run. If not set, defaults to 1.
- `max_prompt_tokens` (integer, required): The maximum number of prompt tokens specified to have been used over the course of the run.
- `max_completion_tokens` (integer, required): The maximum number of completion tokens specified to have been used over the course of the run.
- `truncation_strategy` (object, required): Controls for how a thread will be truncated prior to the run. Use this to control the initial context window of the run.
  - `type` (string, required): The truncation strategy to use for the thread. The default is `auto`. If set to `last_messages`, the thread will be truncated to the n most recent messages in the thread. When set to `auto`, messages in the middle of the thread will be dropped to fit the context length of the model, `max_prompt_tokens`. Enum: 'auto', 'last_messages'.
  - `last_messages` (integer | null, optional)
- `tool_choice` (string | object, required): Controls which (if any) tool is called by the model.
  `none` means the model will not call any tools and instead generates a message.
  `auto` is the default value and means the model can pick between generating a message or calling one or more tools.
  `required` means the model must call one or more tools before responding to the user.
  Specifying a particular tool like `{"type": "file_search"}` or `{"type": "function", "function": {"name": "my_function"}}` forces the model to call that tool.
  - Variant (object):
    - `type` (string, required): The type of the tool. If type is `function`, the function name must be set Enum: 'function', 'code_interpreter', 'file_search'.
    - `function` (object, optional)
      - `name` (string, required): The name of the function to call.
- `parallel_tool_calls` (boolean, required): Whether to enable [parallel function calling](https://platform.openai.com/docs/guides/function-calling#configuring-parallel-function-calling) during tool use. Default: `True`.
- `response_format` (string | object, required): Specifies the format that the model must output. Compatible with [GPT-4o](https://platform.openai.com/docs/models#gpt-4o), [GPT-4 Turbo](https://platform.openai.com/docs/models#gpt-4-turbo-and-gpt-4), and all GPT-3.5 Turbo models since `gpt-3.5-turbo-1106`.
  
  Setting to `{ "type": "json_schema", "json_schema": {...} }` enables Structured Outputs which ensures the model will match your supplied JSON schema. Learn more in the [Structured Outputs guide](https://platform.openai.com/docs/guides/structured-outputs).
  
  Setting to `{ "type": "json_object" }` enables JSON mode, which ensures the message the model generates is valid JSON.
  
  **Important:** when using JSON mode, you **must** also instruct the model to produce JSON yourself via a system or user message. Without this, the model may generate an unending stream of whitespace until the generation reaches the token limit, resulting in a long-running and seemingly "stuck" request. Also note that the message content may be partially cut off if `finish_reason="length"`, which indicates the generation exceeded `max_tokens` or the conversation exceeded the max context length.
  - Variant (object):
    - `type` (string, required): The type of response format being defined. Always `text`. Enum: 'text'.
  - Variant (object):
    - `type` (string, required): The type of response format being defined. Always `json_object`. Enum: 'json_object'.
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

## Returns
The modified [run](object.md) object matching the specified ID.

## Examples
### Default
#### Request (curl)
```bash
curl https://api.openai.com/v1/threads/thread_123/runs/run_123/submit_tool_outputs \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2" \
  -d '{
    "tool_outputs": [
      {
        "tool_call_id": "call_001",
        "output": "70 degrees and sunny."
      }
    ]
  }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

run = client.beta.threads.runs.submit_tool_outputs(
  thread_id="thread_123",
  run_id="run_123",
  tool_outputs=[
    {
      "tool_call_id": "call_001",
      "output": "70 degrees and sunny."
    }
  ]
)

print(run)
```
#### Response
```json
{
  "id": "run_123",
  "object": "thread.run",
  "created_at": 1699075592,
  "assistant_id": "asst_123",
  "thread_id": "thread_123",
  "status": "queued",
  "started_at": 1699075592,
  "expires_at": 1699076192,
  "cancelled_at": null,
  "failed_at": null,
  "completed_at": null,
  "last_error": null,
  "model": "gpt-4o",
  "instructions": null,
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
  "metadata": {},
  "usage": null,
  "temperature": 1.0,
  "top_p": 1.0,
  "max_prompt_tokens": 1000,
  "max_completion_tokens": 1000,
  "truncation_strategy": {
    "type": "auto",
    "last_messages": null
  },
  "response_format": "auto",
  "tool_choice": "auto",
  "parallel_tool_calls": true
}
```
### Streaming
#### Request (curl)
```bash
curl https://api.openai.com/v1/threads/thread_123/runs/run_123/submit_tool_outputs \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2" \
  -d '{
    "tool_outputs": [
      {
        "tool_call_id": "call_001",
        "output": "70 degrees and sunny."
      }
    ],
    "stream": true
  }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

stream = client.beta.threads.runs.submit_tool_outputs(
  thread_id="thread_123",
  run_id="run_123",
  tool_outputs=[
    {
      "tool_call_id": "call_001",
      "output": "70 degrees and sunny."
    }
  ],
  stream=True
)

for event in stream:
  print(event)
```
#### Response
```json
event: thread.run.step.completed
data: {"id":"step_001","object":"thread.run.step","created_at":1710352449,"run_id":"run_123","assistant_id":"asst_123","thread_id":"thread_123","type":"tool_calls","status":"completed","cancelled_at":null,"completed_at":1710352475,"expires_at":1710353047,"failed_at":null,"last_error":null,"step_details":{"type":"tool_calls","tool_calls":[{"id":"call_iWr0kQ2EaYMaxNdl0v3KYkx7","type":"function","function":{"name":"get_current_weather","arguments":"{\"location\":\"San Francisco, CA\",\"unit\":\"fahrenheit\"}","output":"70 degrees and sunny."}}]},"usage":{"prompt_tokens":291,"completion_tokens":24,"total_tokens":315}}

event: thread.run.queued
data: {"id":"run_123","object":"thread.run","created_at":1710352447,"assistant_id":"asst_123","thread_id":"thread_123","status":"queued","started_at":1710352448,"expires_at":1710353047,"cancelled_at":null,"failed_at":null,"completed_at":null,"required_action":null,"last_error":null,"model":"gpt-4o","instructions":null,"tools":[{"type":"function","function":{"name":"get_current_weather","description":"Get the current weather in a given location","parameters":{"type":"object","properties":{"location":{"type":"string","description":"The city and state, e.g. San Francisco, CA"},"unit":{"type":"string","enum":["celsius","fahrenheit"]}},"required":["location"]}}}],"metadata":{},"temperature":1.0,"top_p":1.0,"max_completion_tokens":null,"max_prompt_tokens":null,"truncation_strategy":{"type":"auto","last_messages":null},"incomplete_details":null,"usage":null,"response_format":"auto","tool_choice":"auto","parallel_tool_calls":true}}

event: thread.run.in_progress
data: {"id":"run_123","object":"thread.run","created_at":1710352447,"assistant_id":"asst_123","thread_id":"thread_123","status":"in_progress","started_at":1710352475,"expires_at":1710353047,"cancelled_at":null,"failed_at":null,"completed_at":null,"required_action":null,"last_error":null,"model":"gpt-4o","instructions":null,"tools":[{"type":"function","function":{"name":"get_current_weather","description":"Get the current weather in a given location","parameters":{"type":"object","properties":{"location":{"type":"string","description":"The city and state, e.g. San Francisco, CA"},"unit":{"type":"string","enum":["celsius","fahrenheit"]}},"required":["location"]}}}],"metadata":{},"temperature":1.0,"top_p":1.0,"max_completion_tokens":null,"max_prompt_tokens":null,"truncation_strategy":{"type":"auto","last_messages":null},"incomplete_details":null,"usage":null,"response_format":"auto","tool_choice":"auto","parallel_tool_calls":true}}

event: thread.run.step.created
data: {"id":"step_002","object":"thread.run.step","created_at":1710352476,"run_id":"run_123","assistant_id":"asst_123","thread_id":"thread_123","type":"message_creation","status":"in_progress","cancelled_at":null,"completed_at":null,"expires_at":1710353047,"failed_at":null,"last_error":null,"step_details":{"type":"message_creation","message_creation":{"message_id":"msg_002"}},"usage":null}

event: thread.run.step.in_progress
data: {"id":"step_002","object":"thread.run.step","created_at":1710352476,"run_id":"run_123","assistant_id":"asst_123","thread_id":"thread_123","type":"message_creation","status":"in_progress","cancelled_at":null,"completed_at":null,"expires_at":1710353047,"failed_at":null,"last_error":null,"step_details":{"type":"message_creation","message_creation":{"message_id":"msg_002"}},"usage":null}

event: thread.message.created
data: {"id":"msg_002","object":"thread.message","created_at":1710352476,"assistant_id":"asst_123","thread_id":"thread_123","run_id":"run_123","status":"in_progress","incomplete_details":null,"incomplete_at":null,"completed_at":null,"role":"assistant","content":[],"metadata":{}}

event: thread.message.in_progress
data: {"id":"msg_002","object":"thread.message","created_at":1710352476,"assistant_id":"asst_123","thread_id":"thread_123","run_id":"run_123","status":"in_progress","incomplete_details":null,"incomplete_at":null,"completed_at":null,"role":"assistant","content":[],"metadata":{}}

event: thread.message.delta
data: {"id":"msg_002","object":"thread.message.delta","delta":{"content":[{"index":0,"type":"text","text":{"value":"The","annotations":[]}}]}}

event: thread.message.delta
data: {"id":"msg_002","object":"thread.message.delta","delta":{"content":[{"index":0,"type":"text","text":{"value":" current"}}]}}

event: thread.message.delta
data: {"id":"msg_002","object":"thread.message.delta","delta":{"content":[{"index":0,"type":"text","text":{"value":" weather"}}]}}

...

event: thread.message.delta
data: {"id":"msg_002","object":"thread.message.delta","delta":{"content":[{"index":0,"type":"text","text":{"value":" sunny"}}]}}

event: thread.message.delta
data: {"id":"msg_002","object":"thread.message.delta","delta":{"content":[{"index":0,"type":"text","text":{"value":"."}}]}}

event: thread.message.completed
data: {"id":"msg_002","object":"thread.message","created_at":1710352476,"assistant_id":"asst_123","thread_id":"thread_123","run_id":"run_123","status":"completed","incomplete_details":null,"incomplete_at":null,"completed_at":1710352477,"role":"assistant","content":[{"type":"text","text":{"value":"The current weather in San Francisco, CA is 70 degrees Fahrenheit and sunny.","annotations":[]}}],"metadata":{}}

event: thread.run.step.completed
data: {"id":"step_002","object":"thread.run.step","created_at":1710352476,"run_id":"run_123","assistant_id":"asst_123","thread_id":"thread_123","type":"message_creation","status":"completed","cancelled_at":null,"completed_at":1710352477,"expires_at":1710353047,"failed_at":null,"last_error":null,"step_details":{"type":"message_creation","message_creation":{"message_id":"msg_002"}},"usage":{"prompt_tokens":329,"completion_tokens":18,"total_tokens":347}}

event: thread.run.completed
data: {"id":"run_123","object":"thread.run","created_at":1710352447,"assistant_id":"asst_123","thread_id":"thread_123","status":"completed","started_at":1710352475,"expires_at":null,"cancelled_at":null,"failed_at":null,"completed_at":1710352477,"required_action":null,"last_error":null,"model":"gpt-4o","instructions":null,"tools":[{"type":"function","function":{"name":"get_current_weather","description":"Get the current weather in a given location","parameters":{"type":"object","properties":{"location":{"type":"string","description":"The city and state, e.g. San Francisco, CA"},"unit":{"type":"string","enum":["celsius","fahrenheit"]}},"required":["location"]}}}],"metadata":{},"temperature":1.0,"top_p":1.0,"max_completion_tokens":null,"max_prompt_tokens":null,"truncation_strategy":{"type":"auto","last_messages":null},"incomplete_details":null,"usage":{"prompt_tokens":20,"completion_tokens":11,"total_tokens":31},"response_format":"auto","tool_choice":"auto","parallel_tool_calls":true}}

event: done
data: [DONE]
```
