# response.refusal.done

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/refusal/done

Emitted when refusal text is finalized.

## Properties
- `type` (string, required): The type of the event. Always `response.refusal.done`. Enum: 'response.refusal.done'.
- `item_id` (string, required): The ID of the output item that the refusal text is finalized.
- `output_index` (integer, required): The index of the output item that the refusal text is finalized.
- `content_index` (integer, required): The index of the content part that the refusal text is finalized.
- `refusal` (string, required): The refusal text that is finalized.
- `sequence_number` (integer, required): The sequence number of this event.
