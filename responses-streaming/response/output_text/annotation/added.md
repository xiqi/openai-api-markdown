# response.output_text.annotation.added

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/output_text/annotation/added

Emitted when an annotation is added to output text content.

## Properties
- `type` (string, required): The type of the event. Always 'response.output_text.annotation.added'. Enum: 'response.output_text.annotation.added'.
- `item_id` (string, required): The unique identifier of the item to which the annotation is being added.
- `output_index` (integer, required): The index of the output item in the response's output array.
- `content_index` (integer, required): The index of the content part within the output item.
- `annotation_index` (integer, required): The index of the annotation within the content part.
- `sequence_number` (integer, required): The sequence number of this event.
- `annotation` (object, required): The annotation object being added. (See annotation schema for details.)
