# Delete project role

Source: https://platform.openai.com/docs/api-reference/roles/project/delete

`DELETE /v1/projects/{project_id}/roles/{role_id}`

Deletes a custom role from a project.

## Parameters
- `project_id` (path, string, required): The ID of the project to update.
- `role_id` (path, string, required): The ID of the role to delete.

## Responses
### 200
Project role deleted successfully.
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
curl -X DELETE https://api.openai.com/v1/projects/proj_abc123/roles/role_01J1F8PROJ \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "role.deleted",
    "id": "role_01J1F8PROJ",
    "deleted": true
}
```
