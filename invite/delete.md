# Delete invite

Source: https://platform.openai.com/docs/api-reference/invite/delete

`DELETE /v1/organization/invites/{invite_id}`

Delete an invite. If the invite has already been accepted, it cannot be deleted.

## Parameters
- `invite_id` (path, string, required): The ID of the invite to delete.

## Responses
### 200
Invite deleted successfully.
#### application/json
- `object` (string, required): The object type, which is always `organization.invite.deleted` Enum: 'organization.invite.deleted'.
- `id` (string, required)
- `deleted` (boolean, required)

## Returns
Confirmation that the invite has been deleted

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/invites/invite-abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "organization.invite.deleted",
    "id": "invite-abc",
    "deleted": true
}
```
