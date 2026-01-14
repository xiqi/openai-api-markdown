# The project object

Source: https://platform.openai.com/docs/api-reference/projects/object

Represents an individual project.

## Properties
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `object` (string, required): The object type, which is always `organization.project` Enum: 'organization.project'.
- `name` (string, required): The name of the project. This appears in reporting.
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the project was created.
- `archived_at` (integer | null, optional)
- `status` (string, required): `active` or `archived` Enum: 'active', 'archived'.
