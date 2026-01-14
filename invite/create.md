# Create invite

Source: https://platform.openai.com/docs/api-reference/invite/create

`POST /v1/organization/invites`

Create an invite for a user to the organization. The invite must be accepted by the user before they have access to the organization.

## Request body
### application/json
- `email` (string, required): Send an email to this address
- `role` (string, required): `owner` or `reader` Enum: 'reader', 'owner'.
- `projects` (array<object>, optional): An array of projects to which membership is granted at the same time the org invite is accepted. If omitted, the user will be invited to the default project for compatibility with legacy behavior.
  - Items:
    - `id` (string, required): Project's public ID
    - `role` (string, required): Project membership role Enum: 'member', 'owner'.

## Responses
### 200
User invited successfully.
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
The created [Invite](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/invites \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "email": "anotheruser@example.com",
      "role": "reader",
      "projects": [
        {
          "id": "project-xyz",
          "role": "member"
        },
        {
          "id": "project-abc",
          "role": "owner"
        }
      ]
  }'
```
#### Response
```json
{
  "object": "organization.invite",
  "id": "invite-def",
  "email": "anotheruser@example.com",
  "role": "reader",
  "status": "pending",
  "invited_at": 1711471533,
  "expires_at": 1711471533,
  "accepted_at": null,
  "projects": [
    {
      "id": "project-xyz",
      "role": "member"
    },
    {
      "id": "project-abc",
      "role": "owner"
    }
  ]
}
```
