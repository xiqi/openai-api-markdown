# response.code_interpreter_call_code.delta

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/code_interpreter_call_code/delta

Emitted when a partial code snippet is streamed by the code interpreter.

## Properties
- `type` (string, required): The type of the event. Always `response.code_interpreter_call_code.delta`. Enum: 'response.code_interpreter_call_code.delta'.
- `output_index` (integer, required): The index of the output item in the response for which the code is being streamed.
- `item_id` (string, required): The unique identifier of the code interpreter tool call item.
- `delta` (string, required): The partial code snippet being streamed by the code interpreter.
- `sequence_number` (integer, required): The sequence number of this event, used to order streaming events.
