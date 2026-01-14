# The role object

Source: https://platform.openai.com/docs/api-reference/roles/object

Details about a role that can be assigned through the public Roles API.

## Properties
- `object` (string, required): Always `role`. Enum: 'role'.
- `id` (string, required): Identifier for the role.
- `name` (string, required): Unique name for the role.
- `description` (string | null, required): Optional description of the role.
- `permissions` (array<string>, required): Permissions granted by the role.
- `resource_type` (string, required): Resource type the role is bound to (for example `api.organization` or `api.project`).
- `predefined_role` (boolean, required): Whether the role is predefined and managed by OpenAI.
