# response.mcp_list_tools.completed

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/mcp_list_tools/completed

Emitted when the list of available MCP tools has been successfully retrieved.

## Properties
- `type` (string, required): The type of the event. Always 'response.mcp_list_tools.completed'. Enum: 'response.mcp_list_tools.completed'.
- `item_id` (string, required): The ID of the MCP tool call item that produced this output.
- `output_index` (integer, required): The index of the output item that was processed.
- `sequence_number` (integer, required): The sequence number of this event.
