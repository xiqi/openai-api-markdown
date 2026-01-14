# Delete organization role

Source: https://platform.openai.com/docs/api-reference/roles/delete

`DELETE /v1/organization/roles/{role_id}`

Deletes a custom role from the organization.

## Parameters
- `role_id` (path, string, required): The ID of the role to delete.

## Responses
### 200
Role deleted successfully.
#### application/json
- `object` (string, required): Always `role.deleted`. Enum: 'role.deleted'.
- `id` (string, required): Identifier of the deleted role.
- `deleted` (boolean, required): Whether the role was deleted.

## Returns
Confirmation of the deleted role.

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/roles/role_01J1F8ROLE01 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "role.deleted",
    "id": "role_01J1F8ROLE01",
    "deleted": true
}
```
