# response.mcp_call_arguments.done

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/response/mcp_call_arguments/done

Returned when MCP tool call arguments are finalized during response generation.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.mcp_call_arguments.done`. Enum: 'response.mcp_call_arguments.done'.
- `response_id` (string, required): The ID of the response.
- `item_id` (string, required): The ID of the MCP tool call item.
- `output_index` (integer, required): The index of the output item in the response.
- `arguments` (string, required): The final JSON-encoded arguments string.
