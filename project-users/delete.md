# Delete project user

Source: https://platform.openai.com/docs/api-reference/project-users/delete

`DELETE /v1/organization/projects/{project_id}/users/{user_id}`

Deletes a user from the project.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `user_id` (path, string, required): The ID of the user.

## Responses
### 200
Project user deleted successfully.
#### application/json
- `object` (string, required) Enum: 'organization.project.user.deleted'.
- `id` (string, required)
- `deleted` (boolean, required)
### 400
Error response for various conditions.
#### application/json
- `error` (object, required)
  - `code` (string | null, required)
  - `message` (string, required)
  - `param` (string | null, required)
  - `type` (string, required)

## Returns
Confirmation that project has been deleted or an error in case of an archived project, which has no users

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/projects/proj_abc/users/user_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "organization.project.user.deleted",
    "id": "user_abc",
    "deleted": true
}
```
