# response.code_interpreter_call.in_progress

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/code_interpreter_call/in_progress

Emitted when a code interpreter call is in progress.

## Properties
- `type` (string, required): The type of the event. Always `response.code_interpreter_call.in_progress`. Enum: 'response.code_interpreter_call.in_progress'.
- `output_index` (integer, required): The index of the output item in the response for which the code interpreter call is in progress.
- `item_id` (string, required): The unique identifier of the code interpreter tool call item.
- `sequence_number` (integer, required): The sequence number of this event, used to order streaming events.
