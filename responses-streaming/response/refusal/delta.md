# response.refusal.delta

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/refusal/delta

Emitted when there is a partial refusal text.

## Properties
- `type` (string, required): The type of the event. Always `response.refusal.delta`. Enum: 'response.refusal.delta'.
- `item_id` (string, required): The ID of the output item that the refusal text is added to.
- `output_index` (integer, required): The index of the output item that the refusal text is added to.
- `content_index` (integer, required): The index of the content part that the refusal text is added to.
- `delta` (string, required): The refusal text that is added.
- `sequence_number` (integer, required): The sequence number of this event.
