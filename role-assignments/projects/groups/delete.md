# Unassign project role from group

Source: https://platform.openai.com/docs/api-reference/role-assignments/projects/groups/delete

`DELETE /v1/projects/{project_id}/groups/{group_id}/roles/{role_id}`

Unassigns a project role from a group within a project.

## Parameters
- `project_id` (path, string, required): The ID of the project to modify.
- `group_id` (path, string, required): The ID of the group whose project role assignment should be removed.
- `role_id` (path, string, required): The ID of the project role to remove from the group.

## Responses
### 200
Project role unassigned from the group successfully.
#### application/json
- `object` (string, required): Identifier for the deleted assignment, such as `group.role.deleted` or `user.role.deleted`.
- `deleted` (boolean, required): Whether the assignment was removed.

## Returns
Confirmation of the deleted [group role object](../../objects/group.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/projects/proj_abc123/groups/group_01J1F8ABCDXYZ/roles/role_01J1F8PROJ \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "group.role.deleted",
    "deleted": true
}
```
