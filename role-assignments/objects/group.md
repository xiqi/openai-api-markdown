# The group role object

Source: https://platform.openai.com/docs/api-reference/role-assignments/objects/group

Role assignment linking a group to a role.

## Properties
- `object` (string, required): Always `group.role`. Enum: 'group.role'.
- `group` (object, required): Summary information about a group returned in role assignment responses.
  - `object` (string, required): Always `group`. Enum: 'group'.
  - `id` (string, required): Identifier for the group.
  - `name` (string, required): Display name of the group.
  - `created_at` (integer, required): Unix timestamp (in seconds) when the group was created.
  - `scim_managed` (boolean, required): Whether the group is managed through SCIM.
- `role` (object, required): Details about a role that can be assigned through the public Roles API.
  - `object` (string, required): Always `role`. Enum: 'role'.
  - `id` (string, required): Identifier for the role.
  - `name` (string, required): Unique name for the role.
  - `description` (string | null, required): Optional description of the role.
  - `permissions` (array<string>, required): Permissions granted by the role.
  - `resource_type` (string, required): Resource type the role is bound to (for example `api.organization` or `api.project`).
  - `predefined_role` (boolean, required): Whether the role is predefined and managed by OpenAI.
