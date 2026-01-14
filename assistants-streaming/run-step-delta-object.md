# The run step delta object

Source: https://platform.openai.com/docs/api-reference/assistants-streaming/run-step-delta-object

Represents a run step delta i.e. any changed fields on a run step during streaming.

## Properties
- `id` (string, required): The identifier of the run step, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `thread.run.step.delta`. Enum: 'thread.run.step.delta'.
- `delta` (object, required): The delta containing the fields that have changed on the run step.
  - `step_details` (object, optional): The details of the run step.
    - Variant (object):
      - `type` (string, required): Always `message_creation`. Enum: 'message_creation'.
      - `message_creation` (object, optional)
        - `message_id` (string, optional): The ID of the message that was created by this run step.
    - Variant (object):
      - `type` (string, required): Always `tool_calls`. Enum: 'tool_calls'.
      - `tool_calls` (array<object>, optional): An array of tool calls the run step was involved in. These can be associated with one of three types of tools: `code_interpreter`, `file_search`, or `function`.
