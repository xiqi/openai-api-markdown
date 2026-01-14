# response.function_call_arguments.delta

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/response/function_call_arguments/delta

Returned when the model-generated function call arguments are updated.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.function_call_arguments.delta`. Enum: 'response.function_call_arguments.delta'.
- `response_id` (string, required): The ID of the response.
- `item_id` (string, required): The ID of the function call item.
- `output_index` (integer, required): The index of the output item in the response.
- `call_id` (string, required): The ID of the function call.
- `delta` (string, required): The arguments delta as a JSON string.
