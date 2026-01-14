# Retrieve admin API key

Source: https://platform.openai.com/docs/api-reference/admin-api-keys/listget

`GET /v1/organization/admin_api_keys/{key_id}`

Retrieve a single organization API key

## Parameters
- `key_id` (path, string, required)

## Responses
### 200
Details of the requested API key.
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
The requested [AdminApiKey](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/admin_api_keys/key_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
  "object": "organization.admin_api_key",
  "id": "key_abc",
  "name": "Main Admin Key",
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
  }
}
```
