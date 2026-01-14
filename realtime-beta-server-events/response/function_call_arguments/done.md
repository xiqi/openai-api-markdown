# response.function_call_arguments.done

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/response/function_call_arguments/done

Returned when the model-generated function call arguments are done streaming.
Also emitted when a Response is interrupted, incomplete, or cancelled.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.function_call_arguments.done`. Enum: 'response.function_call_arguments.done'.
- `response_id` (string, required): The ID of the response.
- `item_id` (string, required): The ID of the function call item.
- `output_index` (integer, required): The index of the output item in the response.
- `call_id` (string, required): The ID of the function call.
- `arguments` (string, required): The final arguments as a JSON string.
