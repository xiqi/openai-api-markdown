# response.mcp_call.failed

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/response/mcp_call/failed

Returned when an MCP tool call has failed.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.mcp_call.failed`. Enum: 'response.mcp_call.failed'.
- `output_index` (integer, required): The index of the output item in the response.
- `item_id` (string, required): The ID of the MCP tool call item.
