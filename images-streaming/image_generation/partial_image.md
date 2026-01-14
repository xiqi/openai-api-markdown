# image_generation.partial_image

Source: https://platform.openai.com/docs/api-reference/images-streaming/image_generation/partial_image

Emitted when a partial image is available during image generation streaming.

## Properties
- `type` (string, required): The type of the event. Always `image_generation.partial_image`. Enum: 'image_generation.partial_image'.
- `b64_json` (string, required): Base64-encoded partial image data, suitable for rendering as an image.
- `created_at` (integer, required): The Unix timestamp when the event was created.
- `size` (string, required): The size of the requested image. Enum: '1024x1024', '1024x1536', '1536x1024', 'auto'.
- `quality` (string, required): The quality setting for the requested image. Enum: 'low', 'medium', 'high', 'auto'.
- `background` (string, required): The background setting for the requested image. Enum: 'transparent', 'opaque', 'auto'.
- `output_format` (string, required): The output format for the requested image. Enum: 'png', 'webp', 'jpeg'.
- `partial_image_index` (integer, required): 0-based index for the partial image (streaming).
