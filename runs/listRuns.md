# List runs

Source: https://platform.openai.com/docs/api-reference/runs/listRuns

`GET /v1/threads/{thread_id}/runs`

Returns a list of runs belonging to a thread.

## Parameters
- `thread_id` (path, string, required): The ID of the thread the run belongs to.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `order` (query, string, optional): Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and `desc` for descending order. Enum: 'asc', 'desc'. Default: `desc`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `before` (query, string, optional): A cursor for use in pagination. `before` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, starting with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list.

## Responses
### 200
OK
#### application/json
- `object` (string, required)
- `data` (array<object>, required)
  - Items:
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
          - ...
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
          - ...
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [run](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/threads/thread_abc123/runs \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

runs = client.beta.threads.runs.list(
  "thread_abc123"
)

print(runs)
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "id": "run_abc123",
      "object": "thread.run",
      "created_at": 1699075072,
      "assistant_id": "asst_abc123",
      "thread_id": "thread_abc123",
      "status": "completed",
      "started_at": 1699075072,
      "expires_at": null,
      "cancelled_at": null,
      "failed_at": null,
      "completed_at": 1699075073,
      "last_error": null,
      "model": "gpt-4o",
      "instructions": null,
      "incomplete_details": null,
      "tools": [
        {
          "type": "code_interpreter"
        }
      ],
      "tool_resources": {
        "code_interpreter": {
          "file_ids": [
            "file-abc123",
            "file-abc456"
          ]
        }
      },
      "metadata": {},
      "usage": {
        "prompt_tokens": 123,
        "completion_tokens": 456,
        "total_tokens": 579
      },
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
    },
    {
      "id": "run_abc456",
      "object": "thread.run",
      "created_at": 1699063290,
      "assistant_id": "asst_abc123",
      "thread_id": "thread_abc123",
      "status": "completed",
      "started_at": 1699063290,
      "expires_at": null,
      "cancelled_at": null,
      "failed_at": null,
      "completed_at": 1699063291,
      "last_error": null,
      "model": "gpt-4o",
      "instructions": null,
      "incomplete_details": null,
      "tools": [
        {
          "type": "code_interpreter"
        }
      ],
      "tool_resources": {
        "code_interpreter": {
          "file_ids": [
            "file-abc123",
            "file-abc456"
          ]
        }
      },
      "metadata": {},
      "usage": {
        "prompt_tokens": 123,
        "completion_tokens": 456,
        "total_tokens": 579
      },
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
  ],
  "first_id": "run_abc123",
  "last_id": "run_abc456",
  "has_more": false
}
```
