# response.reasoning_text.delta

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/reasoning_text/delta

Emitted when a delta is added to a reasoning text.

## Properties
- `type` (string, required): The type of the event. Always `response.reasoning_text.delta`. Enum: 'response.reasoning_text.delta'.
- `item_id` (string, required): The ID of the item this reasoning text delta is associated with.
- `output_index` (integer, required): The index of the output item this reasoning text delta is associated with.
- `content_index` (integer, required): The index of the reasoning content part this delta is associated with.
- `delta` (string, required): The text delta that was added to the reasoning content.
- `sequence_number` (integer, required): The sequence number of this event.
