# Modify project user

Source: https://platform.openai.com/docs/api-reference/project-users/modify

`POST /v1/organization/projects/{project_id}/users/{user_id}`

Modifies a user's role in the project.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `user_id` (path, string, required): The ID of the user.

## Request body
### application/json
- `role` (string, required): `owner` or `member` Enum: 'owner', 'member'.

## Responses
### 200
Project user's role updated successfully.
#### application/json
- `object` (string, required): The object type, which is always `organization.project.user` Enum: 'organization.project.user'.
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the user
- `email` (string, required): The email address of the user
- `role` (string, required): `owner` or `member` Enum: 'owner', 'member'.
- `added_at` (integer, required): The Unix timestamp (in seconds) of when the project was added.
### 400
Error response for various conditions.
#### application/json
- `error` (object, required)
  - `code` (string | null, required)
  - `message` (string, required)
  - `param` (string | null, required)
  - `type` (string, required)

## Returns
The updated [ProjectUser](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/projects/proj_abc/users/user_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "role": "owner"
  }'
```
#### Response
```json
{
    "object": "organization.project.user",
    "id": "user_abc",
    "name": "First Last",
    "email": "user@example.com",
    "role": "owner",
    "added_at": 1711471533
}
```
