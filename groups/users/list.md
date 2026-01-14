# List group users

Source: https://platform.openai.com/docs/api-reference/groups/users/list

`GET /v1/organization/groups/{group_id}/users`

Lists the users assigned to a group.

## Parameters
- `group_id` (path, string, required): The ID of the group to inspect.
- `limit` (query, integer, optional): A limit on the number of users to be returned. Limit can range between 0 and 1000, and the default is 100. Default: `100`.
- `after` (query, string, optional): A cursor for use in pagination. Provide the ID of the last user from the previous list response to retrieve the next page.
- `order` (query, string, optional): Specifies the sort order of users in the list. Enum: 'asc', 'desc'. Default: `desc`.

## Responses
### 200
Group users listed successfully.
#### application/json
- `object` (string, required): Always `list`. Enum: 'list'.
- `data` (array<object>, required): Users in the current page.
  - Items:
    - `object` (string, required): The object type, which is always `organization.user` Enum: 'organization.user'.
    - `id` (string, required): The identifier, which can be referenced in API endpoints
    - `name` (string, required): The name of the user
    - `email` (string, required): The email address of the user
    - `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.
    - `added_at` (integer, required): The Unix timestamp (in seconds) of when the user was added.
- `has_more` (boolean, required): Whether more users are available when paginating.
- `next` (string | null, required): Cursor to fetch the next page of results, or `null` when no further users are available.

## Returns
A list of [user objects](../../users/object.md).

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/groups/group_01J1F8ABCDXYZ/users?limit=20 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "object": "organization.user",
            "id": "user_abc123",
            "name": "Ada Lovelace",
            "email": "ada@example.com",
            "role": "owner",
            "added_at": 1711471533
        }
    ],
    "has_more": false,
    "next": null
}
```
