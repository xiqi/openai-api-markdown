# The container file object

Source: https://platform.openai.com/docs/api-reference/container-files/object

## Properties
- `id` (string, required): Unique identifier for the file.
- `object` (string, required): The type of this object (`container.file`).
- `container_id` (string, required): The container this file belongs to.
- `created_at` (integer, required): Unix timestamp (in seconds) when the file was created.
- `bytes` (integer, required): Size of the file in bytes.
- `path` (string, required): Path of the file in the container.
- `source` (string, required): Source of the file (e.g., `user`, `assistant`).
