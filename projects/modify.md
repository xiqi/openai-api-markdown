# Modify project

Source: https://platform.openai.com/docs/api-reference/projects/modify

`POST /v1/organization/projects/{project_id}`

Modifies a project in the organization.

## Parameters
- `project_id` (path, string, required): The ID of the project.

## Request body
### application/json
- `name` (string, required): The updated name of the project, this name appears in reports.

## Responses
### 200
Project updated successfully.
#### application/json
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `object` (string, required): The object type, which is always `organization.project` Enum: 'organization.project'.
- `name` (string, required): The name of the project. This appears in reporting.
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the project was created.
- `archived_at` (integer | null, optional)
- `status` (string, required): `active` or `archived` Enum: 'active', 'archived'.
### 400
Error response when updating the default project.
#### application/json
- `error` (object, required)
  - `code` (string | null, required)
  - `message` (string, required)
  - `param` (string | null, required)
  - `type` (string, required)

## Returns
The updated [Project](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/projects/proj_abc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "name": "Project DEF"
  }'
```
