# List project roles

Source: https://platform.openai.com/docs/api-reference/roles/project/list

`GET /v1/projects/{project_id}/roles`

Lists the roles configured for a project.

## Parameters
- `project_id` (path, string, required): The ID of the project to inspect.
- `limit` (query, integer, optional): A limit on the number of roles to return. Defaults to 1000. Default: `1000`.
- `after` (query, string, optional): Cursor for pagination. Provide the value from the previous response's `next` field to continue listing roles.
- `order` (query, string, optional): Sort order for the returned roles. Enum: 'asc', 'desc'. Default: `asc`.

## Responses
### 200
Project roles listed successfully.
#### application/json
- `object` (string, required): Always `list`. Enum: 'list'.
- `data` (array<object>, required): Roles returned in the current page.
  - Items:
    - `object` (string, required): Always `role`. Enum: 'role'.
    - `id` (string, required): Identifier for the role.
    - `name` (string, required): Unique name for the role.
    - `description` (string | null, required): Optional description of the role.
    - `permissions` (array<string>, required): Permissions granted by the role.
    - `resource_type` (string, required): Resource type the role is bound to (for example `api.organization` or `api.project`).
    - `predefined_role` (boolean, required): Whether the role is predefined and managed by OpenAI.
- `has_more` (boolean, required): Whether more roles are available when paginating.
- `next` (string | null, required): Cursor to fetch the next page of results, or `null` when there are no additional roles.

## Returns
A list of [role objects](../object.md) configured on the project.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/projects/proj_abc123/roles?limit=20 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
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
    ],
    "has_more": false,
    "next": null
}
```
