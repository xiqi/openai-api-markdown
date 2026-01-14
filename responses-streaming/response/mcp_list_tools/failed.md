# response.mcp_list_tools.failed

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/mcp_list_tools/failed

Emitted when the attempt to list available MCP tools has failed.

## Properties
- `type` (string, required): The type of the event. Always 'response.mcp_list_tools.failed'. Enum: 'response.mcp_list_tools.failed'.
- `item_id` (string, required): The ID of the MCP tool call item that failed.
- `output_index` (integer, required): The index of the output item that failed.
- `sequence_number` (integer, required): The sequence number of this event.
