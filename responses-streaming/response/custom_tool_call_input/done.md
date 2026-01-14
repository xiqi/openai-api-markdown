# response.custom_tool_call_input.done

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/custom_tool_call_input/done

Event indicating that input for a custom tool call is complete.

## Properties
- `type` (string, required): The event type identifier. Enum: 'response.custom_tool_call_input.done'.
- `sequence_number` (integer, required): The sequence number of this event.
- `output_index` (integer, required): The index of the output this event applies to.
- `item_id` (string, required): Unique identifier for the API item associated with this event.
- `input` (string, required): The complete input data for the custom tool call.
