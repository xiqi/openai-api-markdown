# response.image_generation_call.generating

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/image_generation_call/generating

Emitted when an image generation tool call is actively generating an image (intermediate state).

## Properties
- `type` (string, required): The type of the event. Always 'response.image_generation_call.generating'. Enum: 'response.image_generation_call.generating'.
- `output_index` (integer, required): The index of the output item in the response's output array.
- `item_id` (string, required): The unique identifier of the image generation item being processed.
- `sequence_number` (integer, required): The sequence number of the image generation item being processed.
