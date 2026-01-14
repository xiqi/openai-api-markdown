# Unassign organization role from group

Source: https://platform.openai.com/docs/api-reference/role-assignments/organization/groups/delete

`DELETE /v1/organization/groups/{group_id}/roles/{role_id}`

Unassigns an organization role from a group within the organization.

## Parameters
- `group_id` (path, string, required): The ID of the group to modify.
- `role_id` (path, string, required): The ID of the organization role to remove from the group.

## Responses
### 200
Organization role unassigned from the group successfully.
#### application/json
- `object` (string, required): Identifier for the deleted assignment, such as `group.role.deleted` or `user.role.deleted`.
- `deleted` (boolean, required): Whether the assignment was removed.

## Returns
Confirmation of the deleted [group role object](../../objects/group.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/groups/group_01J1F8ABCDXYZ/roles/role_01J1F8ROLE01 \
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
