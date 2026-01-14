# Retrieve invite

Source: https://platform.openai.com/docs/api-reference/invite/retrieve

`GET /v1/organization/invites/{invite_id}`

Retrieves an invite.

## Parameters
- `invite_id` (path, string, required): The ID of the invite to retrieve.

## Responses
### 200
Invite retrieved successfully.
#### application/json
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

## Returns
The [Invite](object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/invites/invite-abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
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
```
