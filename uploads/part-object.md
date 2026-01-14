# The upload part object

Source: https://platform.openai.com/docs/api-reference/uploads/part-object

The upload Part represents a chunk of bytes we can add to an Upload object.

## Properties
- `id` (string, required): The upload Part unique identifier, which can be referenced in API endpoints.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the Part was created.
- `upload_id` (string, required): The ID of the Upload object that this Part was added to.
- `object` (string, required): The object type, which is always `upload.part`. Enum: 'upload.part'.
