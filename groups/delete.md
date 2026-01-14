# Delete group

Source: https://platform.openai.com/docs/api-reference/groups/delete

`DELETE /v1/organization/groups/{group_id}`

Deletes a group from the organization.

## Parameters
- `group_id` (path, string, required): The ID of the group to delete.

## Responses
### 200
Group deleted successfully.
#### application/json
- `object` (string, required): Always `group.deleted`. Enum: 'group.deleted'.
- `id` (string, required): Identifier of the deleted group.
- `deleted` (boolean, required): Whether the group was deleted.

## Returns
Confirmation of the deleted group.

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/groups/group_01J1F8ABCDXYZ \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "group.deleted",
    "id": "group_01J1F8ABCDXYZ",
    "deleted": true
}
```
