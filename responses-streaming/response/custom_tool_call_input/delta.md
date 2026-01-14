# response.custom_tool_call_input.delta

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/custom_tool_call_input/delta

Event representing a delta (partial update) to the input of a custom tool call.

## Properties
- `type` (string, required): The event type identifier. Enum: 'response.custom_tool_call_input.delta'.
- `sequence_number` (integer, required): The sequence number of this event.
- `output_index` (integer, required): The index of the output this delta applies to.
- `item_id` (string, required): Unique identifier for the API item associated with this event.
- `delta` (string, required): The incremental input data (delta) for the custom tool call.
