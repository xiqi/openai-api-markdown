# response.reasoning_summary_text.delta

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/reasoning_summary_text/delta

Emitted when a delta is added to a reasoning summary text.

## Properties
- `type` (string, required): The type of the event. Always `response.reasoning_summary_text.delta`. Enum: 'response.reasoning_summary_text.delta'.
- `item_id` (string, required): The ID of the item this summary text delta is associated with.
- `output_index` (integer, required): The index of the output item this summary text delta is associated with.
- `summary_index` (integer, required): The index of the summary part within the reasoning summary.
- `delta` (string, required): The text delta that was added to the summary.
- `sequence_number` (integer, required): The sequence number of this event.
