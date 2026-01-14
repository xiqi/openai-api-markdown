# response.output_text.done

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/response/output_text/done

Returned when the text value of an "output_text" content part is done streaming. Also
emitted when a Response is interrupted, incomplete, or cancelled.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.output_text.done`. Enum: 'response.output_text.done'.
- `response_id` (string, required): The ID of the response.
- `item_id` (string, required): The ID of the item.
- `output_index` (integer, required): The index of the output item in the response.
- `content_index` (integer, required): The index of the content part in the item's content array.
- `text` (string, required): The final text content.
