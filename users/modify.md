# Modify user

Source: https://platform.openai.com/docs/api-reference/users/modify

`POST /v1/organization/users/{user_id}`

Modifies a user's role in the organization.

## Parameters
- `user_id` (path, string, required): The ID of the user.

## Request body
### application/json
- `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.

## Responses
### 200
User role updated successfully.
#### application/json
- `object` (string, required): The object type, which is always `organization.user` Enum: 'organization.user'.
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the user
- `email` (string, required): The email address of the user
- `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.
- `added_at` (integer, required): The Unix timestamp (in seconds) of when the user was added.

## Returns
The updated [User](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/users/user_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "role": "owner"
  }'
```
#### Response
```json
{
    "object": "organization.user",
    "id": "user_abc",
    "name": "First Last",
    "email": "user@example.com",
    "role": "owner",
    "added_at": 1711471533
}
```
