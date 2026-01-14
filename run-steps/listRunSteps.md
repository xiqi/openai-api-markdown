# List run steps

Source: https://platform.openai.com/docs/api-reference/run-steps/listRunSteps

`GET /v1/threads/{thread_id}/runs/{run_id}/steps`

Returns a list of run steps belonging to a run.

## Parameters
- `thread_id` (path, string, required): The ID of the thread the run and run steps belong to.
- `run_id` (path, string, required): The ID of the run the run steps belong to.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `order` (query, string, optional): Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and `desc` for descending order. Enum: 'asc', 'desc'. Default: `desc`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `before` (query, string, optional): A cursor for use in pagination. `before` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, starting with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list.
- `include[]` (query, array<string>, optional): A list of additional fields to include in the response. Currently the only supported value is `step_details.tool_calls[*].file_search.results[*].content` to fetch the file search result content.
  
  See the [file search tool documentation](https://platform.openai.com/docs/assistants/tools/file-search#customizing-file-search-settings) for more information.

## Responses
### 200
OK
#### application/json
- `object` (string, required)
- `data` (array<object>, required)
  - Items:
    - `id` (string, required): The identifier of the run step, which can be referenced in API endpoints.
    - `object` (string, required): The object type, which is always `thread.run.step`. Enum: 'thread.run.step'.
    - `created_at` (integer, required): The Unix timestamp (in seconds) for when the run step was created.
    - `assistant_id` (string, required): The ID of the [assistant](../assistants/index.md) associated with the run step.
    - `thread_id` (string, required): The ID of the [thread](../threads/index.md) that was run.
    - `run_id` (string, required): The ID of the [run](../runs/index.md) that this run step is a part of.
    - `type` (string, required): The type of run step, which can be either `message_creation` or `tool_calls`. Enum: 'message_creation', 'tool_calls'.
    - `status` (string, required): The status of the run step, which can be either `in_progress`, `cancelled`, `failed`, `completed`, or `expired`. Enum: 'in_progress', 'cancelled', 'failed', 'completed', 'expired'.
    - `step_details` (object, required): The details of the run step.
      - Variant (object):
        - `type` (string, required): Always `message_creation`. Enum: 'message_creation'.
        - `message_creation` (object, required)
          - ...
      - Variant (object):
        - `type` (string, required): Always `tool_calls`. Enum: 'tool_calls'.
        - `tool_calls` (array<object>, required): An array of tool calls the run step was involved in. These can be associated with one of three types of tools: `code_interpreter`, `file_search`, or `function`.
    - `last_error` (object | null, required)
      - Variant (object):
        - `code` (string, required): One of `server_error` or `rate_limit_exceeded`. Enum: 'server_error', 'rate_limit_exceeded'.
        - `message` (string, required): A human-readable description of the error.
    - `expired_at` (integer | null, required)
    - `cancelled_at` (integer | null, required)
    - `failed_at` (integer | null, required)
    - `completed_at` (integer | null, required)
    - `metadata` (object | null, required)
    - `usage` (object | null, required)
      - Variant (object):
        - `completion_tokens` (integer, required): Number of completion tokens used over the course of the run step.
        - `prompt_tokens` (integer, required): Number of prompt tokens used over the course of the run step.
        - `total_tokens` (integer, required): Total number of tokens used (prompt + completion).
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [run step](step-object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/threads/thread_abc123/runs/run_abc123/steps \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -H "OpenAI-Beta: assistants=v2"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

run_steps = client.beta.threads.runs.steps.list(
    thread_id="thread_abc123",
    run_id="run_abc123"
)

print(run_steps)
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "id": "step_abc123",
      "object": "thread.run.step",
      "created_at": 1699063291,
      "run_id": "run_abc123",
      "assistant_id": "asst_abc123",
      "thread_id": "thread_abc123",
      "type": "message_creation",
      "status": "completed",
      "cancelled_at": null,
      "completed_at": 1699063291,
      "expired_at": null,
      "failed_at": null,
      "last_error": null,
      "step_details": {
        "type": "message_creation",
        "message_creation": {
          "message_id": "msg_abc123"
        }
      },
      "usage": {
        "prompt_tokens": 123,
        "completion_tokens": 456,
        "total_tokens": 579
      }
    }
  ],
  "first_id": "step_abc123",
  "last_id": "step_abc456",
  "has_more": false
}
```
