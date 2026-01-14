# Unassign project role from user

Source: https://platform.openai.com/docs/api-reference/role-assignments/projects/users/delete

`DELETE /v1/projects/{project_id}/users/{user_id}/roles/{role_id}`

Unassigns a project role from a user within a project.

## Parameters
- `project_id` (path, string, required): The ID of the project to modify.
- `user_id` (path, string, required): The ID of the user whose project role assignment should be removed.
- `role_id` (path, string, required): The ID of the project role to remove from the user.

## Responses
### 200
Project role unassigned from the user successfully.
#### application/json
- `object` (string, required): Identifier for the deleted assignment, such as `group.role.deleted` or `user.role.deleted`.
- `deleted` (boolean, required): Whether the assignment was removed.

## Returns
Confirmation of the deleted [user role object](../../objects/user.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/projects/proj_abc123/users/user_abc123/roles/role_01J1F8PROJ \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "user.role.deleted",
    "deleted": true
}
```
