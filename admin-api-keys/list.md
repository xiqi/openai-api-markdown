# List all organization and project API keys.

Source: https://platform.openai.com/docs/api-reference/admin-api-keys/list

`GET /v1/organization/admin_api_keys`

List organization API keys

## Parameters
- `after` (query, string, optional)
- `order` (query, string, optional) Enum: 'asc', 'desc'. Default: `asc`.
- `limit` (query, integer, optional) Default: `20`.

## Responses
### 200
A list of organization API keys.
#### application/json
- `object` (string, optional)
- `data` (array<object>, optional)
  - Items:
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
- `has_more` (boolean, optional)
- `first_id` (string, optional)
- `last_id` (string, optional)

## Returns
A list of admin and project API key objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/admin_api_keys?after=key_abc&limit=20 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "object": "organization.admin_api_key",
      "id": "key_abc",
      "name": "Main Admin Key",
      "redacted_value": "sk-admin...def",
      "created_at": 1711471533,
      "last_used_at": 1711471534,
      "owner": {
        "type": "service_account",
        "object": "organization.service_account",
        "id": "sa_456",
        "name": "My Service Account",
        "created_at": 1711471533,
        "role": "member"
      }
    }
  ],
  "first_id": "key_abc",
  "last_id": "key_abc",
  "has_more": false
}
```
