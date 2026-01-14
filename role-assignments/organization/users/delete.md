# Unassign organization role from user

Source: https://platform.openai.com/docs/api-reference/role-assignments/organization/users/delete

`DELETE /v1/organization/users/{user_id}/roles/{role_id}`

Unassigns an organization role from a user within the organization.

## Parameters
- `user_id` (path, string, required): The ID of the user to modify.
- `role_id` (path, string, required): The ID of the organization role to remove from the user.

## Responses
### 200
Organization role unassigned from the user successfully.
#### application/json
- `object` (string, required): Identifier for the deleted assignment, such as `group.role.deleted` or `user.role.deleted`.
- `deleted` (boolean, required): Whether the assignment was removed.

## Returns
Confirmation of the deleted [user role object](../../objects/user.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/users/user_abc123/roles/role_01J1F8ROLE01 \
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
