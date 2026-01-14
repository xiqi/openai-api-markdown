# List project users

Source: https://platform.openai.com/docs/api-reference/project-users/list

`GET /v1/organization/projects/{project_id}/users`

Returns a list of users in the project.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.

## Responses
### 200
Project users listed successfully.
#### application/json
- `object` (string, required)
- `data` (array<object>, required)
  - Items:
    - `object` (string, required): The object type, which is always `organization.project.user` Enum: 'organization.project.user'.
    - `id` (string, required): The identifier, which can be referenced in API endpoints
    - `name` (string, required): The name of the user
    - `email` (string, required): The email address of the user
    - `role` (string, required): `owner` or `member` Enum: 'owner', 'member'.
    - `added_at` (integer, required): The Unix timestamp (in seconds) of when the project was added.
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)
### 400
Error response when project is archived.
#### application/json
- `error` (object, required)
  - `code` (string | null, required)
  - `message` (string, required)
  - `param` (string | null, required)
  - `type` (string, required)

## Returns
A list of [ProjectUser](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/projects/proj_abc/users?after=user_abc&limit=20 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "object": "organization.project.user",
            "id": "user_abc",
            "name": "First Last",
            "email": "user@example.com",
            "role": "owner",
            "added_at": 1711471533
        }
    ],
    "first_id": "user-abc",
    "last_id": "user-xyz",
    "has_more": false
}
```
