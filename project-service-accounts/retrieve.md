# Retrieve project service account

Source: https://platform.openai.com/docs/api-reference/project-service-accounts/retrieve

`GET /v1/organization/projects/{project_id}/service_accounts/{service_account_id}`

Retrieves a service account in the project.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `service_account_id` (path, string, required): The ID of the service account.

## Responses
### 200
Project service account retrieved successfully.
#### application/json
- `object` (string, required): The object type, which is always `organization.project.service_account` Enum: 'organization.project.service_account'.
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the service account
- `role` (string, required): `owner` or `member` Enum: 'owner', 'member'.
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the service account was created

## Returns
The [ProjectServiceAccount](object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/projects/proj_abc/service_accounts/svc_acct_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "organization.project.service_account",
    "id": "svc_acct_abc",
    "name": "Service Account",
    "role": "owner",
    "created_at": 1711471533
}
```
