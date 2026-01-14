# mcp_list_tools.failed

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/mcp_list_tools/failed

Returned when listing MCP tools has failed for an item.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `mcp_list_tools.failed`. Enum: 'mcp_list_tools.failed'.
- `item_id` (string, required): The ID of the MCP list tools item.
