# response.image_generation_call.completed

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/image_generation_call/completed

Emitted when an image generation tool call has completed and the final image is available.

## Properties
- `type` (string, required): The type of the event. Always 'response.image_generation_call.completed'. Enum: 'response.image_generation_call.completed'.
- `output_index` (integer, required): The index of the output item in the response's output array.
- `sequence_number` (integer, required): The sequence number of this event.
- `item_id` (string, required): The unique identifier of the image generation item being processed.
