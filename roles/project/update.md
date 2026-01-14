# Update project role

Source: https://platform.openai.com/docs/api-reference/roles/project/update

`POST /v1/projects/{project_id}/roles/{role_id}`

Updates an existing project role.

## Parameters
- `project_id` (path, string, required): The ID of the project to update.
- `role_id` (path, string, required): The ID of the role to update.

## Request body
### application/json
- `permissions` (array<string> | null, optional): Updated set of permissions for the role.
- `description` (string | null, optional): New description for the role.
- `role_name` (string | null, optional): New name for the role.

## Responses
### 200
Project role updated successfully.
#### application/json
- `object` (string, required): Always `role`. Enum: 'role'.
- `id` (string, required): Identifier for the role.
- `name` (string, required): Unique name for the role.
- `description` (string | null, required): Optional description of the role.
- `permissions` (array<string>, required): Permissions granted by the role.
- `resource_type` (string, required): Resource type the role is bound to (for example `api.organization` or `api.project`).
- `predefined_role` (boolean, required): Whether the role is predefined and managed by OpenAI.

## Returns
The updated [role object](../object.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/projects/proj_abc123/roles/role_01J1F8PROJ \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "role_name": "API Project Key Manager",
      "permissions": [
          "api.organization.projects.api_keys.read",
          "api.organization.projects.api_keys.write"
      ],
      "description": "Allows managing API keys for the project"
  }'
```
#### Response
```json
{
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
```
