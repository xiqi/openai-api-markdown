# response.reasoning_summary_text.done

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/reasoning_summary_text/done

Emitted when a reasoning summary text is completed.

## Properties
- `type` (string, required): The type of the event. Always `response.reasoning_summary_text.done`. Enum: 'response.reasoning_summary_text.done'.
- `item_id` (string, required): The ID of the item this summary text is associated with.
- `output_index` (integer, required): The index of the output item this summary text is associated with.
- `summary_index` (integer, required): The index of the summary part within the reasoning summary.
- `text` (string, required): The full text of the completed reasoning summary.
- `sequence_number` (integer, required): The sequence number of this event.
