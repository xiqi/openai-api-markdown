# Add group user

Source: https://platform.openai.com/docs/api-reference/groups/users/add

`POST /v1/organization/groups/{group_id}/users`

Adds a user to a group.

## Parameters
- `group_id` (path, string, required): The ID of the group to update.

## Request body
### application/json
- `user_id` (string, required): Identifier of the user to add to the group.

## Responses
### 200
User added to the group successfully.
#### application/json
- `object` (string, required): Always `group.user`. Enum: 'group.user'.
- `user_id` (string, required): Identifier of the user that was added.
- `group_id` (string, required): Identifier of the group the user was added to.

## Returns
The created [group user object](assignment-object.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/groups/group_01J1F8ABCDXYZ/users \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "user_id": "user_abc123"
  }'
```
#### Response
```json
{
    "object": "group.user",
    "user_id": "user_abc123",
    "group_id": "group_01J1F8ABCDXYZ"
}
```
