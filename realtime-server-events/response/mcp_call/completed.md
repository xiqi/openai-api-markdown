# response.mcp_call.completed

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/response/mcp_call/completed

Returned when an MCP tool call has completed successfully.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.mcp_call.completed`. Enum: 'response.mcp_call.completed'.
- `output_index` (integer, required): The index of the output item in the response.
- `item_id` (string, required): The ID of the MCP tool call item.
