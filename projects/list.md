# List projects

Source: https://platform.openai.com/docs/api-reference/projects/list

`GET /v1/organization/projects`

Returns a list of projects.

## Parameters
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `include_archived` (query, boolean, optional): If `true` returns all projects including those that have been `archived`. Archived projects are not included by default. Default: `False`.

## Responses
### 200
Projects listed successfully.
#### application/json
- `object` (string, required) Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `id` (string, required): The identifier, which can be referenced in API endpoints
    - `object` (string, required): The object type, which is always `organization.project` Enum: 'organization.project'.
    - `name` (string, required): The name of the project. This appears in reporting.
    - `created_at` (integer, required): The Unix timestamp (in seconds) of when the project was created.
    - `archived_at` (integer | null, optional)
    - `status` (string, required): `active` or `archived` Enum: 'active', 'archived'.
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [Project](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/projects?after=proj_abc&limit=20&include_archived=false \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "id": "proj_abc",
            "object": "organization.project",
            "name": "Project example",
            "created_at": 1711471533,
            "archived_at": null,
            "status": "active"
        }
    ],
    "first_id": "proj-abc",
    "last_id": "proj-xyz",
    "has_more": false
}
```
