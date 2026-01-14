# List users

Source: https://platform.openai.com/docs/api-reference/users/list

`GET /v1/organization/users`

Lists all of the users in the organization.

## Parameters
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `emails` (query, array<string>, optional): Filter by the email address of users.

## Responses
### 200
Users listed successfully.
#### application/json
- `object` (string, required) Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `object` (string, required): The object type, which is always `organization.user` Enum: 'organization.user'.
    - `id` (string, required): The identifier, which can be referenced in API endpoints
    - `name` (string, required): The name of the user
    - `email` (string, required): The email address of the user
    - `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.
    - `added_at` (integer, required): The Unix timestamp (in seconds) of when the user was added.
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [User](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/users?after=user_abc&limit=20 \
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
