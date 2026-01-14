# response.mcp_call.in_progress

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/response/mcp_call/in_progress

Returned when an MCP tool call has started and is in progress.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.mcp_call.in_progress`. Enum: 'response.mcp_call.in_progress'.
- `output_index` (integer, required): The index of the output item in the response.
- `item_id` (string, required): The ID of the MCP tool call item.
