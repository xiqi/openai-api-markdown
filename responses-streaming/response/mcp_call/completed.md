# response.mcp_call.completed

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/mcp_call/completed

Emitted when an MCP  tool call has completed successfully.

## Properties
- `type` (string, required): The type of the event. Always 'response.mcp_call.completed'. Enum: 'response.mcp_call.completed'.
- `item_id` (string, required): The ID of the MCP tool call item that completed.
- `output_index` (integer, required): The index of the output item that completed.
- `sequence_number` (integer, required): The sequence number of this event.
