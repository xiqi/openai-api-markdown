# response.mcp_list_tools.in_progress

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/mcp_list_tools/in_progress

Emitted when the system is in the process of retrieving the list of available MCP tools.

## Properties
- `type` (string, required): The type of the event. Always 'response.mcp_list_tools.in_progress'. Enum: 'response.mcp_list_tools.in_progress'.
- `item_id` (string, required): The ID of the MCP tool call item that is being processed.
- `output_index` (integer, required): The index of the output item that is being processed.
- `sequence_number` (integer, required): The sequence number of this event.
