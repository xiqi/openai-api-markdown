# Delete admin API key

Source: https://platform.openai.com/docs/api-reference/admin-api-keys/delete

`DELETE /v1/organization/admin_api_keys/{key_id}`

Delete an organization admin API key

## Parameters
- `key_id` (path, string, required)

## Responses
### 200
Confirmation that the API key was deleted.
#### application/json
- `id` (string, optional)
- `object` (string, optional)
- `deleted` (boolean, optional)

## Returns
A confirmation object indicating the key was deleted.

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/admin_api_keys/key_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
  "id": "key_abc",
  "object": "organization.admin_api_key.deleted",
  "deleted": true
}
```
