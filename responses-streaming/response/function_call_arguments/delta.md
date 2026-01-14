# response.function_call_arguments.delta

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/function_call_arguments/delta

Emitted when there is a partial function-call arguments delta.

## Properties
- `type` (string, required): The type of the event. Always `response.function_call_arguments.delta`. Enum: 'response.function_call_arguments.delta'.
- `item_id` (string, required): The ID of the output item that the function-call arguments delta is added to.
- `output_index` (integer, required): The index of the output item that the function-call arguments delta is added to.
- `sequence_number` (integer, required): The sequence number of this event.
- `delta` (string, required): The function-call arguments delta that is added.
