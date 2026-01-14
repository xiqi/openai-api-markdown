# response.image_generation_call.in_progress

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/image_generation_call/in_progress

Emitted when an image generation tool call is in progress.

## Properties
- `type` (string, required): The type of the event. Always 'response.image_generation_call.in_progress'. Enum: 'response.image_generation_call.in_progress'.
- `output_index` (integer, required): The index of the output item in the response's output array.
- `item_id` (string, required): The unique identifier of the image generation item being processed.
- `sequence_number` (integer, required): The sequence number of the image generation item being processed.
