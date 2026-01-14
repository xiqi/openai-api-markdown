# List project rate limits

Source: https://platform.openai.com/docs/api-reference/project-rate-limits/list

`GET /v1/organization/projects/{project_id}/rate_limits`

Returns the rate limits per model for a project.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. The default is 100. Default: `100`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `before` (query, string, optional): A cursor for use in pagination. `before` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, beginning with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list.

## Responses
### 200
Project rate limits listed successfully.
#### application/json
- `object` (string, required) Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `object` (string, required): The object type, which is always `project.rate_limit` Enum: 'project.rate_limit'.
    - `id` (string, required): The identifier, which can be referenced in API endpoints.
    - `model` (string, required): The model this rate limit applies to.
    - `max_requests_per_1_minute` (integer, required): The maximum requests per minute.
    - `max_tokens_per_1_minute` (integer, required): The maximum tokens per minute.
    - `max_images_per_1_minute` (integer, optional): The maximum images per minute. Only present for relevant models.
    - `max_audio_megabytes_per_1_minute` (integer, optional): The maximum audio megabytes per minute. Only present for relevant models.
    - `max_requests_per_1_day` (integer, optional): The maximum requests per day. Only present for relevant models.
    - `batch_1_day_max_input_tokens` (integer, optional): The maximum batch input tokens per day. Only present for relevant models.
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [ProjectRateLimit](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/projects/proj_abc/rate_limits?after=rl_xxx&limit=20 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
          "object": "project.rate_limit",
          "id": "rl-ada",
          "model": "ada",
          "max_requests_per_1_minute": 600,
          "max_tokens_per_1_minute": 150000,
          "max_images_per_1_minute": 10
        }
    ],
    "first_id": "rl-ada",
    "last_id": "rl-ada",
    "has_more": false
}
```
