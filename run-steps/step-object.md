# The run step object

Source: https://platform.openai.com/docs/api-reference/run-steps/step-object

Represents a step in execution of a run.

## Properties
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
      - `message_id` (string, required): The ID of the message that was created by this run step.
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
