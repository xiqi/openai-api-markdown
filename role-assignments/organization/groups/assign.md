# Assign organization role to group

Source: https://platform.openai.com/docs/api-reference/role-assignments/organization/groups/assign

`POST /v1/organization/groups/{group_id}/roles`

Assigns an organization role to a group within the organization.

## Parameters
- `group_id` (path, string, required): The ID of the group that should receive the organization role.

## Request body
### application/json
- `role_id` (string, required): Identifier of the role to assign.

## Responses
### 200
Organization role assigned to the group successfully.
#### application/json
- `object` (string, required): Always `group.role`. Enum: 'group.role'.
- `group` (object, required): Summary information about a group returned in role assignment responses.
  - `object` (string, required): Always `group`. Enum: 'group'.
  - `id` (string, required): Identifier for the group.
  - `name` (string, required): Display name of the group.
  - `created_at` (integer, required): Unix timestamp (in seconds) when the group was created.
  - `scim_managed` (boolean, required): Whether the group is managed through SCIM.
- `role` (object, required): Details about a role that can be assigned through the public Roles API.
  - `object` (string, required): Always `role`. Enum: 'role'.
  - `id` (string, required): Identifier for the role.
  - `name` (string, required): Unique name for the role.
  - `description` (string | null, required): Optional description of the role.
  - `permissions` (array<string>, required): Permissions granted by the role.
  - `resource_type` (string, required): Resource type the role is bound to (for example `api.organization` or `api.project`).
  - `predefined_role` (boolean, required): Whether the role is predefined and managed by OpenAI.

## Returns
The created [group role object](../../objects/group.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/groups/group_01J1F8ABCDXYZ/roles \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "role_id": "role_01J1F8ROLE01"
  }'
```
#### Response
```json
{
    "object": "group.role",
    "group": {
        "object": "group",
        "id": "group_01J1F8ABCDXYZ",
        "name": "Support Team",
        "created_at": 1711471533,
        "scim_managed": false
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
