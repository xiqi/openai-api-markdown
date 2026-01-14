# response.mcp_call_arguments.done

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/mcp_call_arguments/done

Emitted when the arguments for an MCP tool call are finalized.

## Properties
- `type` (string, required): The type of the event. Always 'response.mcp_call_arguments.done'. Enum: 'response.mcp_call_arguments.done'.
- `output_index` (integer, required): The index of the output item in the response's output array.
- `item_id` (string, required): The unique identifier of the MCP tool call item being processed.
- `arguments` (string, required): A JSON string containing the finalized arguments for the MCP tool call.
- `sequence_number` (integer, required): The sequence number of this event.
