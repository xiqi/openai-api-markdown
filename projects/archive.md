# Archive project

Source: https://platform.openai.com/docs/api-reference/projects/archive

`POST /v1/organization/projects/{project_id}/archive`

Archives a project in the organization. Archived projects cannot be used or updated.

## Parameters
- `project_id` (path, string, required): The ID of the project.

## Responses
### 200
Project archived successfully.
#### application/json
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `object` (string, required): The object type, which is always `organization.project` Enum: 'organization.project'.
- `name` (string, required): The name of the project. This appears in reporting.
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the project was created.
- `archived_at` (integer | null, optional)
- `status` (string, required): `active` or `archived` Enum: 'active', 'archived'.

## Returns
The archived [Project](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/projects/proj_abc/archive \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "id": "proj_abc",
    "object": "organization.project",
    "name": "Project DEF",
    "created_at": 1711471533,
    "archived_at": 1711471533,
    "status": "archived"
}
```
