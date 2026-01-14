# Delete project API key

Source: https://platform.openai.com/docs/api-reference/project-api-keys/delete

`DELETE /v1/organization/projects/{project_id}/api_keys/{key_id}`

Deletes an API key from the project.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `key_id` (path, string, required): The ID of the API key.

## Responses
### 200
Project API key deleted successfully.
#### application/json
- `object` (string, required) Enum: 'organization.project.api_key.deleted'.
- `id` (string, required)
- `deleted` (boolean, required)
### 400
Error response for various conditions.
#### application/json
- `error` (object, required)
  - `code` (string | null, required)
  - `message` (string, required)
  - `param` (string | null, required)
  - `type` (string, required)

## Returns
Confirmation of the key's deletion or an error if the key belonged to a service account

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/projects/proj_abc/api_keys/key_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "organization.project.api_key.deleted",
    "id": "key_abc",
    "deleted": true
}
```
