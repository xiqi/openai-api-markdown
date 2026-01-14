# Assign organization role to user

Source: https://platform.openai.com/docs/api-reference/role-assignments/organization/users/assign

`POST /v1/organization/users/{user_id}/roles`

Assigns an organization role to a user within the organization.

## Parameters
- `user_id` (path, string, required): The ID of the user that should receive the organization role.

## Request body
### application/json
- `role_id` (string, required): Identifier of the role to assign.

## Responses
### 200
Organization role assigned to the user successfully.
#### application/json
- `object` (string, required): Always `user.role`. Enum: 'user.role'.
- `user` (object, required): Represents an individual `user` within an organization.
  - `object` (string, required): The object type, which is always `organization.user` Enum: 'organization.user'.
  - `id` (string, required): The identifier, which can be referenced in API endpoints
  - `name` (string, required): The name of the user
  - `email` (string, required): The email address of the user
  - `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.
  - `added_at` (integer, required): The Unix timestamp (in seconds) of when the user was added.
- `role` (object, required): Details about a role that can be assigned through the public Roles API.
  - `object` (string, required): Always `role`. Enum: 'role'.
  - `id` (string, required): Identifier for the role.
  - `name` (string, required): Unique name for the role.
  - `description` (string | null, required): Optional description of the role.
  - `permissions` (array<string>, required): Permissions granted by the role.
  - `resource_type` (string, required): Resource type the role is bound to (for example `api.organization` or `api.project`).
  - `predefined_role` (boolean, required): Whether the role is predefined and managed by OpenAI.

## Returns
The created [user role object](../../objects/user.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/users/user_abc123/roles \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "role_id": "role_01J1F8ROLE01"
  }'
```
#### Response
```json
{
    "object": "user.role",
    "user": {
        "object": "organization.user",
        "id": "user_abc123",
        "name": "Ada Lovelace",
        "email": "ada@example.com",
        "role": "owner",
        "added_at": 1711470000
    },
    "role": {
        "object": "role",
        "id": "role_01J1F8ROLE01",
        "name": "API Group Manager",
        "description": "Allows managing organization groups",
        "permissions": [
            "api.groups.read",
            "api.groups.write"
        ],
        "resource_type": "api.organization",
        "predefined_role": false
    }
}
```
