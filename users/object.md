# The user object

Source: https://platform.openai.com/docs/api-reference/users/object

Represents an individual `user` within an organization.

## Properties
- `object` (string, required): The object type, which is always `organization.user` Enum: 'organization.user'.
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the user
- `email` (string, required): The email address of the user
- `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.
- `added_at` (integer, required): The Unix timestamp (in seconds) of when the user was added.
