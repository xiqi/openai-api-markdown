# List invites

Source: https://platform.openai.com/docs/api-reference/invite/list

`GET /v1/organization/invites`

Returns a list of invites in the organization.

## Parameters
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.

## Responses
### 200
Invites listed successfully.
#### application/json
- `object` (string, required): The object type, which is always `list` Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `object` (string, required): The object type, which is always `organization.invite` Enum: 'organization.invite'.
    - `id` (string, required): The identifier, which can be referenced in API endpoints
    - `email` (string, required): The email address of the individual to whom the invite was sent
    - `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.
    - `status` (string, required): `accepted`,`expired`, or `pending` Enum: 'accepted', 'expired', 'pending'.
    - `invited_at` (integer, required): The Unix timestamp (in seconds) of when the invite was sent.
    - `expires_at` (integer, required): The Unix timestamp (in seconds) of when the invite expires.
    - `accepted_at` (integer, optional): The Unix timestamp (in seconds) of when the invite was accepted.
    - `projects` (array<object>, optional): The projects that were granted membership upon acceptance of the invite.
      - Items:
        - `id` (string, optional): Project's public ID
        - `role` (string, optional): Project membership role Enum: 'member', 'owner'.
- `first_id` (string, optional): The first `invite_id` in the retrieved `list`
- `last_id` (string, optional): The last `invite_id` in the retrieved `list`
- `has_more` (boolean, optional): The `has_more` property is used for pagination to indicate there are additional results.

## Returns
A list of [Invite](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/invites?after=invite-abc&limit=20 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "object": "organization.invite",
      "id": "invite-abc",
      "email": "user@example.com",
      "role": "owner",
      "status": "accepted",
      "invited_at": 1711471533,
      "expires_at": 1711471533,
      "accepted_at": 1711471533
    }
  ],
  "first_id": "invite-abc",
  "last_id": "invite-abc",
  "has_more": false
}
```
