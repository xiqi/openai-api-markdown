# response.image_generation_call.partial_image

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/image_generation_call/partial_image

Emitted when a partial image is available during image generation streaming.

## Properties
- `type` (string, required): The type of the event. Always 'response.image_generation_call.partial_image'. Enum: 'response.image_generation_call.partial_image'.
- `output_index` (integer, required): The index of the output item in the response's output array.
- `item_id` (string, required): The unique identifier of the image generation item being processed.
- `sequence_number` (integer, required): The sequence number of the image generation item being processed.
- `partial_image_index` (integer, required): 0-based index for the partial image (backend is 1-based, but this is 0-based for the user).
- `partial_image_b64` (string, required): Base64-encoded partial image data, suitable for rendering as an image.
