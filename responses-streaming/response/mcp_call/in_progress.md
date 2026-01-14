# response.mcp_call.in_progress

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/mcp_call/in_progress

Emitted when an MCP  tool call is in progress.

## Properties
- `type` (string, required): The type of the event. Always 'response.mcp_call.in_progress'. Enum: 'response.mcp_call.in_progress'.
- `sequence_number` (integer, required): The sequence number of this event.
- `output_index` (integer, required): The index of the output item in the response's output array.
- `item_id` (string, required): The unique identifier of the MCP tool call item being processed.
