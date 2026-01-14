# Create admin API key

Source: https://platform.openai.com/docs/api-reference/admin-api-keys/create

`POST /v1/organization/admin_api_keys`

Create an organization admin API key

## Request body
### application/json
- `name` (string, required)

## Responses
### 200
The newly created admin API key.
#### application/json
- `object` (string, required): The object type, which is always `organization.admin_api_key`
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the API key
- `redacted_value` (string, required): The redacted value of the API key
- `value` (string, optional): The value of the API key. Only shown on create.
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the API key was created
- `last_used_at` (integer | null, required)
- `owner` (object, required)
  - `type` (string, optional): Always `user`
  - `object` (string, optional): The object type, which is always organization.user
  - `id` (string, optional): The identifier, which can be referenced in API endpoints
  - `name` (string, optional): The name of the user
  - `created_at` (integer, optional): The Unix timestamp (in seconds) of when the user was created
  - `role` (string, optional): Always `owner`

## Returns
The created [AdminApiKey](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/admin_api_keys \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "name": "New Admin Key"
  }'
```
#### Response
```json
{
  "object": "organization.admin_api_key",
  "id": "key_xyz",
  "name": "New Admin Key",
  "redacted_value": "sk-admin...xyz",
  "created_at": 1711471533,
  "last_used_at": 1711471534,
  "owner": {
    "type": "user",
    "object": "organization.user",
    "id": "user_123",
    "name": "John Doe",
    "created_at": 1711471533,
    "role": "owner"
  },
  "value": "sk-admin-1234abcd"
}
```
