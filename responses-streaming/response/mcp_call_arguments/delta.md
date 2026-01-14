# response.mcp_call_arguments.delta

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/mcp_call_arguments/delta

Emitted when there is a delta (partial update) to the arguments of an MCP tool call.

## Properties
- `type` (string, required): The type of the event. Always 'response.mcp_call_arguments.delta'. Enum: 'response.mcp_call_arguments.delta'.
- `output_index` (integer, required): The index of the output item in the response's output array.
- `item_id` (string, required): The unique identifier of the MCP tool call item being processed.
- `delta` (string, required): A JSON string containing the partial update to the arguments for the MCP tool call.
- `sequence_number` (integer, required): The sequence number of this event.
