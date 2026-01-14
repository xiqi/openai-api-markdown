# The fine-tuned model checkpoint permission object

Source: https://platform.openai.com/docs/api-reference/fine-tuning/permission-object

The `checkpoint.permission` object represents a permission for a fine-tuned model checkpoint.

## Properties
- `id` (string, required): The permission identifier, which can be referenced in the API endpoints.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the permission was created.
- `project_id` (string, required): The project identifier that the permission is for.
- `object` (string, required): The object type, which is always "checkpoint.permission". Enum: 'checkpoint.permission'.
