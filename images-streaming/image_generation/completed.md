# image_generation.completed

Source: https://platform.openai.com/docs/api-reference/images-streaming/image_generation/completed

Emitted when image generation has completed and the final image is available.

## Properties
- `type` (string, required): The type of the event. Always `image_generation.completed`. Enum: 'image_generation.completed'.
- `b64_json` (string, required): Base64-encoded image data, suitable for rendering as an image.
- `created_at` (integer, required): The Unix timestamp when the event was created.
- `size` (string, required): The size of the generated image. Enum: '1024x1024', '1024x1536', '1536x1024', 'auto'.
- `quality` (string, required): The quality setting for the generated image. Enum: 'low', 'medium', 'high', 'auto'.
- `background` (string, required): The background setting for the generated image. Enum: 'transparent', 'opaque', 'auto'.
- `output_format` (string, required): The output format for the generated image. Enum: 'png', 'webp', 'jpeg'.
- `usage` (object, required): For the GPT image models only, the token usage information for the image generation.
  - `total_tokens` (integer, required): The total number of tokens (images and text) used for the image generation.
  - `input_tokens` (integer, required): The number of tokens (images and text) in the input prompt.
  - `output_tokens` (integer, required): The number of image tokens in the output image.
  - `input_tokens_details` (object, required): The input tokens detailed information for the image generation.
    - `text_tokens` (integer, required): The number of text tokens in the input prompt.
    - `image_tokens` (integer, required): The number of image tokens in the input prompt.
