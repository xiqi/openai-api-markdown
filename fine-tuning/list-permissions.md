# List checkpoint permissions

Source: https://platform.openai.com/docs/api-reference/fine-tuning/list-permissions

`GET /v1/fine_tuning/checkpoints/{fine_tuned_model_checkpoint}/permissions`

**NOTE:** This endpoint requires an [admin API key](../admin-api-keys).

Organization owners can use this endpoint to view all permissions for a fine-tuned model checkpoint.

## Parameters
- `fine_tuned_model_checkpoint` (path, string, required): The ID of the fine-tuned model checkpoint to get permissions for.
- `project_id` (query, string, optional): The ID of the project to get permissions for.
- `after` (query, string, optional): Identifier for the last permission ID from the previous pagination request.
- `limit` (query, integer, optional): Number of permissions to retrieve. Default: `10`.
- `order` (query, string, optional): The order in which to retrieve permissions. Enum: 'ascending', 'descending'. Default: `descending`.

## Responses
### 200
OK
#### application/json
- `data` (array<object>, required)
  - Items:
    - `id` (string, required): The permission identifier, which can be referenced in the API endpoints.
    - `created_at` (integer, required): The Unix timestamp (in seconds) for when the permission was created.
    - `project_id` (string, required): The project identifier that the permission is for.
    - `object` (string, required): The object type, which is always "checkpoint.permission". Enum: 'checkpoint.permission'.
- `object` (string, required) Enum: 'list'.
- `first_id` (string | null, optional)
- `last_id` (string | null, optional)
- `has_more` (boolean, required)

## Returns
A list of fine-tuned model checkpoint [permission objects](permission-object.md) for a fine-tuned model checkpoint.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/fine_tuning/checkpoints/ft:gpt-4o-mini-2024-07-18:org:weather:B7R9VjQd/permissions \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "object": "checkpoint.permission",
      "id": "cp_zc4Q7MP6XxulcVzj4MZdwsAB",
      "created_at": 1721764867,
      "project_id": "proj_abGMw1llN8IrBb6SvvY5A1iH"
    },
    {
      "object": "checkpoint.permission",
      "id": "cp_enQCFmOTGj3syEpYVhBRLTSy",
      "created_at": 1721764800,
      "project_id": "proj_iqGMw1llN8IrBb6SvvY5A1oF"
    },
  ],
  "first_id": "cp_zc4Q7MP6XxulcVzj4MZdwsAB",
  "last_id": "cp_enQCFmOTGj3syEpYVhBRLTSy",
  "has_more": false
}
```
