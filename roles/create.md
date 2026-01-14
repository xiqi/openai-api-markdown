# Create organization role

Source: https://platform.openai.com/docs/api-reference/roles/create

`POST /v1/organization/roles`

Creates a custom role for the organization.

## Request body
### application/json
- `role_name` (string, required): Unique name for the role.
- `permissions` (array<string>, required): Permissions to grant to the role.
- `description` (string | null, optional): Optional description of the role.

## Responses
### 200
Role created successfully.
#### application/json
- `object` (string, required): Always `role`. Enum: 'role'.
- `id` (string, required): Identifier for the role.
- `name` (string, required): Unique name for the role.
- `description` (string | null, required): Optional description of the role.
- `permissions` (array<string>, required): Permissions granted by the role.
- `resource_type` (string, required): Resource type the role is bound to (for example `api.organization` or `api.project`).
- `predefined_role` (boolean, required): Whether the role is predefined and managed by OpenAI.

## Returns
The created [role object](object.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/roles \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "role_name": "API Group Manager",
      "permissions": [
          "api.groups.read",
          "api.groups.write"
      ],
      "description": "Allows managing organization groups"
  }'
```
#### Response
```json
{
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
```
