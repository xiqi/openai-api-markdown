# response.reasoning_summary_part.added

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/reasoning_summary_part/added

Emitted when a new reasoning summary part is added.

## Properties
- `type` (string, required): The type of the event. Always `response.reasoning_summary_part.added`. Enum: 'response.reasoning_summary_part.added'.
- `item_id` (string, required): The ID of the item this summary part is associated with.
- `output_index` (integer, required): The index of the output item this summary part is associated with.
- `summary_index` (integer, required): The index of the summary part within the reasoning summary.
- `sequence_number` (integer, required): The sequence number of this event.
- `part` (object, required): The summary part that was added.
  - `type` (string, required): The type of the summary part. Always `summary_text`. Enum: 'summary_text'.
  - `text` (string, required): The text of the summary part.
