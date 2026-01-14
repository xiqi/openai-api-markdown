# List project service accounts

Source: https://platform.openai.com/docs/api-reference/project-service-accounts/list

`GET /v1/organization/projects/{project_id}/service_accounts`

Returns a list of service accounts in the project.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.

## Responses
### 200
Project service accounts listed successfully.
#### application/json
- `object` (string, required) Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `object` (string, required): The object type, which is always `organization.project.service_account` Enum: 'organization.project.service_account'.
    - `id` (string, required): The identifier, which can be referenced in API endpoints
    - `name` (string, required): The name of the service account
    - `role` (string, required): `owner` or `member` Enum: 'owner', 'member'.
    - `created_at` (integer, required): The Unix timestamp (in seconds) of when the service account was created
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)
### 400
Error response when project is archived.
#### application/json
- `error` (object, required)
  - `code` (string | null, required)
  - `message` (string, required)
  - `param` (string | null, required)
  - `type` (string, required)

## Returns
A list of [ProjectServiceAccount](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/projects/proj_abc/service_accounts?after=custom_id&limit=20 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "object": "organization.project.service_account",
            "id": "svc_acct_abc",
            "name": "Service Account",
            "role": "owner",
            "created_at": 1711471533
        }
    ],
    "first_id": "svc_acct_abc",
    "last_id": "svc_acct_xyz",
    "has_more": false
}
```
