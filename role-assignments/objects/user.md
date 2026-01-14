# The user role object

Source: https://platform.openai.com/docs/api-reference/role-assignments/objects/user

Role assignment linking a user to a role.

## Properties
- `object` (string, required): Always `user.role`. Enum: 'user.role'.
- `user` (object, required): Represents an individual `user` within an organization.
  - `object` (string, required): The object type, which is always `organization.user` Enum: 'organization.user'.
  - `id` (string, required): The identifier, which can be referenced in API endpoints
  - `name` (string, required): The name of the user
  - `email` (string, required): The email address of the user
  - `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.
  - `added_at` (integer, required): The Unix timestamp (in seconds) of when the user was added.
- `role` (object, required): Details about a role that can be assigned through the public Roles API.
  - `object` (string, required): Always `role`. Enum: 'role'.
  - `id` (string, required): Identifier for the role.
  - `name` (string, required): Unique name for the role.
  - `description` (string | null, required): Optional description of the role.
  - `permissions` (array<string>, required): Permissions granted by the role.
  - `resource_type` (string, required): Resource type the role is bound to (for example `api.organization` or `api.project`).
  - `predefined_role` (boolean, required): Whether the role is predefined and managed by OpenAI.
