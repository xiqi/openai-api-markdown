# The project user object

Source: https://platform.openai.com/docs/api-reference/project-users/object

Represents an individual user in a project.

## Properties
- `object` (string, required): The object type, which is always `organization.project.user` Enum: 'organization.project.user'.
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the user
- `email` (string, required): The email address of the user
- `role` (string, required): `owner` or `member` Enum: 'owner', 'member'.
- `added_at` (integer, required): The Unix timestamp (in seconds) of when the project was added.
