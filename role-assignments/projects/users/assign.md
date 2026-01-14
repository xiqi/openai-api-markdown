# Assign project role to user

Source: https://platform.openai.com/docs/api-reference/role-assignments/projects/users/assign

`POST /v1/projects/{project_id}/users/{user_id}/roles`

Assigns a project role to a user within a project.

## Parameters
- `project_id` (path, string, required): The ID of the project to update.
- `user_id` (path, string, required): The ID of the user that should receive the project role.

## Request body
### application/json
- `role_id` (string, required): Identifier of the role to assign.

## Responses
### 200
Project role assigned to the user successfully.
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
curl -X POST https://api.openai.com/v1/projects/proj_abc123/users/user_abc123/roles \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "role_id": "role_01J1F8PROJ"
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
        "id": "role_01J1F8PROJ",
        "name": "API Project Key Manager",
        "description": "Allows managing API keys for the project",
        "permissions": [
            "api.organization.projects.api_keys.read",
            "api.organization.projects.api_keys.write"
        ],
        "resource_type": "api.project",
        "predefined_role": false
    }
}
```
