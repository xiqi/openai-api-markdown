# mcp_list_tools.completed

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/mcp_list_tools/completed

Returned when listing MCP tools has completed for an item.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `mcp_list_tools.completed`. Enum: 'mcp_list_tools.completed'.
- `item_id` (string, required): The ID of the MCP list tools item.
