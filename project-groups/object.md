# The project group object

Source: https://platform.openai.com/docs/api-reference/project-groups/object

Details about a group's membership in a project.

## Properties
- `object` (string, required): Always `project.group`. Enum: 'project.group'.
- `project_id` (string, required): Identifier of the project.
- `group_id` (string, required): Identifier of the group that has access to the project.
- `group_name` (string, required): Display name of the group.
- `created_at` (integer, required): Unix timestamp (in seconds) when the group was granted project access.
