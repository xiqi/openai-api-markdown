# Retrieve user

Source: https://platform.openai.com/docs/api-reference/users/retrieve

`GET /v1/organization/users/{user_id}`

Retrieves a user by their identifier.

## Parameters
- `user_id` (path, string, required): The ID of the user.

## Responses
### 200
User retrieved successfully.
#### application/json
- `object` (string, required): The object type, which is always `organization.user` Enum: 'organization.user'.
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the user
- `email` (string, required): The email address of the user
- `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.
- `added_at` (integer, required): The Unix timestamp (in seconds) of when the user was added.

## Returns
The [User](object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/users/user_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
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
