# Delete project service account

Source: https://platform.openai.com/docs/api-reference/project-service-accounts/delete

`DELETE /v1/organization/projects/{project_id}/service_accounts/{service_account_id}`

Deletes a service account from the project.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `service_account_id` (path, string, required): The ID of the service account.

## Responses
### 200
Project service account deleted successfully.
#### application/json
- `object` (string, required) Enum: 'organization.project.service_account.deleted'.
- `id` (string, required)
- `deleted` (boolean, required)

## Returns
Confirmation of service account being deleted, or an error in case of an archived project, which has no service accounts

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/projects/proj_abc/service_accounts/svc_acct_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "organization.project.service_account.deleted",
    "id": "svc_acct_abc",
    "deleted": true
}
```
