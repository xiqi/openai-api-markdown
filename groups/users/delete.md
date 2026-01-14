# Remove group user

Source: https://platform.openai.com/docs/api-reference/groups/users/delete

`DELETE /v1/organization/groups/{group_id}/users/{user_id}`

Removes a user from a group.

## Parameters
- `group_id` (path, string, required): The ID of the group to update.
- `user_id` (path, string, required): The ID of the user to remove from the group.

## Responses
### 200
User removed from the group successfully.
#### application/json
- `object` (string, required): Always `group.user.deleted`. Enum: 'group.user.deleted'.
- `deleted` (boolean, required): Whether the group membership was removed.

## Returns
Confirmation of the deleted [group user object](assignment-object.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/groups/group_01J1F8ABCDXYZ/users/user_abc123 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "group.user.deleted",
    "deleted": true
}
```
