# Remove project group

Source: https://platform.openai.com/docs/api-reference/project-groups/delete

`DELETE /v1/organization/projects/{project_id}/groups/{group_id}`

Revokes a group's access to a project.

## Parameters
- `project_id` (path, string, required): The ID of the project to update.
- `group_id` (path, string, required): The ID of the group to remove from the project.

## Responses
### 200
Group removed from the project successfully.
#### application/json
- `object` (string, required): Always `project.group.deleted`. Enum: 'project.group.deleted'.
- `deleted` (boolean, required): Whether the group membership in the project was removed.

## Returns
Confirmation of the deleted project group.

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/projects/proj_abc123/groups/group_01J1F8ABCDXYZ \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "project.group.deleted",
    "deleted": true
}
```
