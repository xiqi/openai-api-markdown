# Update group

Source: https://platform.openai.com/docs/api-reference/groups/update

`POST /v1/organization/groups/{group_id}`

Updates a group's information.

## Parameters
- `group_id` (path, string, required): The ID of the group to update.

## Request body
### application/json
- `name` (string, required): New display name for the group.

## Responses
### 200
Group updated successfully.
#### application/json
- `id` (string, required): Identifier for the group.
- `name` (string, required): Updated display name for the group.
- `created_at` (integer, required): Unix timestamp (in seconds) when the group was created.
- `is_scim_managed` (boolean, required): Whether the group is managed through SCIM and controlled by your identity provider.

## Returns
The updated [group object](object.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/groups/group_01J1F8ABCDXYZ \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "name": "Escalations"
  }'
```
#### Response
```json
{
    "id": "group_01J1F8ABCDXYZ",
    "name": "Escalations",
    "created_at": 1711471533,
    "is_scim_managed": false
}
```
