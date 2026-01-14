# Create project service account

Source: https://platform.openai.com/docs/api-reference/project-service-accounts/create

`POST /v1/organization/projects/{project_id}/service_accounts`

Creates a new service account in the project. This also returns an unredacted API key for the service account.

## Parameters
- `project_id` (path, string, required): The ID of the project.

## Request body
### application/json
- `name` (string, required): The name of the service account being created.

## Responses
### 200
Project service account created successfully.
#### application/json
- `object` (string, required) Enum: 'organization.project.service_account'.
- `id` (string, required)
- `name` (string, required)
- `role` (string, required): Service accounts can only have one role of type `member` Enum: 'member'.
- `created_at` (integer, required)
- `api_key` (object, required)
  - `object` (string, required): The object type, which is always `organization.project.service_account.api_key` Enum: 'organization.project.service_account.api_key'.
  - `value` (string, required)
  - `name` (string, required)
  - `created_at` (integer, required)
  - `id` (string, required)
### 400
Error response when project is archived.
#### application/json
- `error` (object, required)
  - `code` (string | null, required)
  - `message` (string, required)
  - `param` (string | null, required)
  - `type` (string, required)

## Returns
The created [ProjectServiceAccount](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/projects/proj_abc/service_accounts \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "name": "Production App"
  }'
```
#### Response
```json
{
    "object": "organization.project.service_account",
    "id": "svc_acct_abc",
    "name": "Production App",
    "role": "member",
    "created_at": 1711471533,
    "api_key": {
        "object": "organization.project.service_account.api_key",
        "value": "sk-abcdefghijklmnop123",
        "name": "Secret Key",
        "created_at": 1711471533,
        "id": "key_abc"
    }
}
```
