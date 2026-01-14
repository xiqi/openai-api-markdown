# Create group

Source: https://platform.openai.com/docs/api-reference/groups/create

`POST /v1/organization/groups`

Creates a new group in the organization.

## Request body
### application/json
- `name` (string, required): Human readable name for the group.

## Responses
### 200
Group created successfully.
#### application/json
- `id` (string, required): Identifier for the group.
- `name` (string, required): Display name of the group.
- `created_at` (integer, required): Unix timestamp (in seconds) when the group was created.
- `is_scim_managed` (boolean, required): Whether the group is managed through SCIM and controlled by your identity provider.

## Returns
The created [group object](object.md).

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/groups \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "name": "Support Team"
  }'
```
#### Response
```json
{
    "object": "group",
    "id": "group_01J1F8ABCDXYZ",
    "name": "Support Team",
    "created_at": 1711471533,
    "is_scim_managed": false
}
```
