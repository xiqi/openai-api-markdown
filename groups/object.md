# The group object

Source: https://platform.openai.com/docs/api-reference/groups/object

Summary information about a group returned in role assignment responses.

## Properties
- `object` (string, required): Always `group`. Enum: 'group'.
- `id` (string, required): Identifier for the group.
- `name` (string, required): Display name of the group.
- `created_at` (integer, required): Unix timestamp (in seconds) when the group was created.
- `scim_managed` (boolean, required): Whether the group is managed through SCIM.
