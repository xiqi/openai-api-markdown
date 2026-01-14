# response.mcp_call_arguments.delta

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/response/mcp_call_arguments/delta

Returned when MCP tool call arguments are updated during response generation.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.mcp_call_arguments.delta`. Enum: 'response.mcp_call_arguments.delta'.
- `response_id` (string, required): The ID of the response.
- `item_id` (string, required): The ID of the MCP tool call item.
- `output_index` (integer, required): The index of the output item in the response.
- `delta` (string, required): The JSON-encoded arguments delta.
- `obfuscation` (string | null, optional)
