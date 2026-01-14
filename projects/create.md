# Create project

Source: https://platform.openai.com/docs/api-reference/projects/create

`POST /v1/organization/projects`

Create a new project in the organization. Projects can be created and archived, but cannot be deleted.

## Request body
### application/json
- `name` (string, required): The friendly name of the project, this name appears in reports.
- `geography` (string, optional): Create the project with the specified data residency region. Your organization must have access to Data residency functionality in order to use. See [data residency controls](https://platform.openai.com/docs/guides/your-data#data-residency-controls) to review the functionality and limitations of setting this field. Enum: 'US', 'EU', 'JP', 'IN', 'KR', 'CA', 'AU', 'SG'.

## Responses
### 200
Project created successfully.
#### application/json
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `object` (string, required): The object type, which is always `organization.project` Enum: 'organization.project'.
- `name` (string, required): The name of the project. This appears in reporting.
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the project was created.
- `archived_at` (integer | null, optional)
- `status` (string, required): `active` or `archived` Enum: 'active', 'archived'.

## Returns
The created [Project](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/projects \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "name": "Project ABC"
  }'
```
#### Response
```json
{
    "id": "proj_abc",
    "object": "organization.project",
    "name": "Project ABC",
    "created_at": 1711471533,
    "archived_at": null,
    "status": "active"
}
```
