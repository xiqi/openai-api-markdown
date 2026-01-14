# mcp_list_tools.in_progress

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/mcp_list_tools/in_progress

Returned when listing MCP tools is in progress for an item.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `mcp_list_tools.in_progress`. Enum: 'mcp_list_tools.in_progress'.
- `item_id` (string, required): The ID of the MCP list tools item.
