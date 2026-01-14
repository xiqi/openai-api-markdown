# Delete user

Source: https://platform.openai.com/docs/api-reference/users/delete

`DELETE /v1/organization/users/{user_id}`

Deletes a user from the organization.

## Parameters
- `user_id` (path, string, required): The ID of the user.

## Responses
### 200
User deleted successfully.
#### application/json
- `object` (string, required) Enum: 'organization.user.deleted'.
- `id` (string, required)
- `deleted` (boolean, required)

## Returns
Confirmation of the deleted user

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/users/user_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "organization.user.deleted",
    "id": "user_abc",
    "deleted": true
}
```
