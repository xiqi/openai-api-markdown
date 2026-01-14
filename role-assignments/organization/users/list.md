# List user organization role assignments

Source: https://platform.openai.com/docs/api-reference/role-assignments/organization/users/list

`GET /v1/organization/users/{user_id}/roles`

Lists the organization roles assigned to a user within the organization.

## Parameters
- `user_id` (path, string, required): The ID of the user to inspect.
- `limit` (query, integer, optional): A limit on the number of organization role assignments to return.
- `after` (query, string, optional): Cursor for pagination. Provide the value from the previous response's `next` field to continue listing organization roles.
- `order` (query, string, optional): Sort order for the returned organization roles. Enum: 'asc', 'desc'.

## Responses
### 200
User organization role assignments listed successfully.
#### application/json
- `object` (string, required): Always `list`. Enum: 'list'.
- `data` (array<object>, required): Role assignments returned in the current page.
  - Items:
    - `id` (string, required): Identifier for the role.
    - `name` (string, required): Name of the role.
    - `permissions` (array<string>, required): Permissions associated with the role.
    - `resource_type` (string, required): Resource type the role applies to.
    - `predefined_role` (boolean, required): Whether the role is predefined by OpenAI.
    - `description` (string | null, required): Description of the role.
    - `created_at` (integer | null, required): When the role was created.
    - `updated_at` (integer | null, required): When the role was last updated.
    - `created_by` (string | null, required): Identifier of the actor who created the role.
    - `created_by_user_obj` (object | null, required): User details for the actor that created the role, when available.
    - `metadata` (object | null, required): Arbitrary metadata stored on the role.
- `has_more` (boolean, required): Whether additional assignments are available when paginating.
- `next` (string | null, required): Cursor to fetch the next page of results, or `null` when there are no more assignments.

## Returns
A list of [role objects](../../../roles/object.md).

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/users/user_abc123/roles \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "id": "role_01J1F8ROLE01",
            "name": "API Group Manager",
            "permissions": [
                "api.groups.read",
                "api.groups.write"
            ],
            "resource_type": "api.organization",
            "predefined_role": false,
            "description": "Allows managing organization groups",
            "created_at": 1711471533,
            "updated_at": 1711472599,
            "created_by": "user_abc123",
            "created_by_user_obj": {
                "id": "user_abc123",
                "name": "Ada Lovelace",
                "email": "ada@example.com"
            },
            "metadata": {}
        }
    ],
    "has_more": false,
    "next": null
}
```
