# response.mcp_call.failed

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/mcp_call/failed

Emitted when an MCP  tool call has failed.

## Properties
- `type` (string, required): The type of the event. Always 'response.mcp_call.failed'. Enum: 'response.mcp_call.failed'.
- `item_id` (string, required): The ID of the MCP tool call item that failed.
- `output_index` (integer, required): The index of the output item that failed.
- `sequence_number` (integer, required): The sequence number of this event.
