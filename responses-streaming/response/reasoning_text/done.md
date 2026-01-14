# response.reasoning_text.done

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/reasoning_text/done

Emitted when a reasoning text is completed.

## Properties
- `type` (string, required): The type of the event. Always `response.reasoning_text.done`. Enum: 'response.reasoning_text.done'.
- `item_id` (string, required): The ID of the item this reasoning text is associated with.
- `output_index` (integer, required): The index of the output item this reasoning text is associated with.
- `content_index` (integer, required): The index of the reasoning content part.
- `text` (string, required): The full text of the completed reasoning content.
- `sequence_number` (integer, required): The sequence number of this event.
