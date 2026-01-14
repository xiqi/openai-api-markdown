# Add project group

Source: https://platform.openai.com/docs/api-reference/project-groups/add

`POST /v1/organization/projects/{project_id}/groups`

Grants a group access to a project.

## Parameters
- `project_id` (path, string, required): The ID of the project to update.

## Request body
### application/json
- `group_id` (string, required): Identifier of the group to add to the project.
- `role` (string, required): Identifier of the project role to grant to the group.

## Responses
### 200
Group granted access to the project successfully.
#### application/json
- `object` (string, required): Always `project.group`. Enum: 'project.group'.
- `project_id` (string, required): Identifier of the project.
- `group_id` (string, required): Identifier of the group that has access to the project.
- `group_name` (string, required): Display name of the group.
- `created_at` (integer, required): Unix timestamp (in seconds) when the group was granted project access.

## Returns
The created [project group object](object.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/projects/proj_abc123/groups \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "group_id": "group_01J1F8ABCDXYZ",
      "role": "role_01J1F8PROJ"
  }'
```
#### Response
```json
{
    "object": "project.group",
    "project_id": "proj_abc123",
    "group_id": "group_01J1F8ABCDXYZ",
    "group_name": "Support Team",
    "created_at": 1711471533
}
```
