# List project groups

Source: https://platform.openai.com/docs/api-reference/project-groups/list

`GET /v1/organization/projects/{project_id}/groups`

Lists the groups that have access to a project.

## Parameters
- `project_id` (path, string, required): The ID of the project to inspect.
- `limit` (query, integer, optional): A limit on the number of project groups to return. Defaults to 20. Default: `20`.
- `after` (query, string, optional): Cursor for pagination. Provide the ID of the last group from the previous response to fetch the next page.
- `order` (query, string, optional): Sort order for the returned groups. Enum: 'asc', 'desc'. Default: `asc`.

## Responses
### 200
Project groups listed successfully.
#### application/json
- `object` (string, required): Always `list`. Enum: 'list'.
- `data` (array<object>, required): Project group memberships returned in the current page.
  - Items:
    - `object` (string, required): Always `project.group`. Enum: 'project.group'.
    - `project_id` (string, required): Identifier of the project.
    - `group_id` (string, required): Identifier of the group that has access to the project.
    - `group_name` (string, required): Display name of the group.
    - `created_at` (integer, required): Unix timestamp (in seconds) when the group was granted project access.
- `has_more` (boolean, required): Whether additional project group memberships are available.
- `next` (string | null, required): Cursor to fetch the next page of results, or `null` when there are no more results.

## Returns
A list of [project group objects](object.md).

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/projects/proj_abc123/groups?limit=20 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "object": "project.group",
            "project_id": "proj_abc123",
            "group_id": "group_01J1F8ABCDXYZ",
            "group_name": "Support Team",
            "created_at": 1711471533
        }
    ],
    "has_more": false,
    "next": null
}
```
