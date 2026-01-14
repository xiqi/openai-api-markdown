# response.function_call_arguments.done

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/function_call_arguments/done

Emitted when function-call arguments are finalized.

## Properties
- `type` (string, required) Enum: 'response.function_call_arguments.done'.
- `item_id` (string, required): The ID of the item.
- `name` (string, required): The name of the function that was called.
- `output_index` (integer, required): The index of the output item.
- `sequence_number` (integer, required): The sequence number of this event.
- `arguments` (string, required): The function-call arguments.
