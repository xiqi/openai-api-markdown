# response.code_interpreter_call_code.done

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/code_interpreter_call_code/done

Emitted when the code snippet is finalized by the code interpreter.

## Properties
- `type` (string, required): The type of the event. Always `response.code_interpreter_call_code.done`. Enum: 'response.code_interpreter_call_code.done'.
- `output_index` (integer, required): The index of the output item in the response for which the code is finalized.
- `item_id` (string, required): The unique identifier of the code interpreter tool call item.
- `code` (string, required): The final code snippet output by the code interpreter.
- `sequence_number` (integer, required): The sequence number of this event, used to order streaming events.
