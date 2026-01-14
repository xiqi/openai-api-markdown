# Modify project rate limit

Source: https://platform.openai.com/docs/api-reference/project-rate-limits/update

`POST /v1/organization/projects/{project_id}/rate_limits/{rate_limit_id}`

Updates a project rate limit.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `rate_limit_id` (path, string, required): The ID of the rate limit.

## Request body
### application/json
- `max_requests_per_1_minute` (integer, optional): The maximum requests per minute.
- `max_tokens_per_1_minute` (integer, optional): The maximum tokens per minute.
- `max_images_per_1_minute` (integer, optional): The maximum images per minute. Only relevant for certain models.
- `max_audio_megabytes_per_1_minute` (integer, optional): The maximum audio megabytes per minute. Only relevant for certain models.
- `max_requests_per_1_day` (integer, optional): The maximum requests per day. Only relevant for certain models.
- `batch_1_day_max_input_tokens` (integer, optional): The maximum batch input tokens per day. Only relevant for certain models.

## Responses
### 200
Project rate limit updated successfully.
#### application/json
- `object` (string, required): The object type, which is always `project.rate_limit` Enum: 'project.rate_limit'.
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `model` (string, required): The model this rate limit applies to.
- `max_requests_per_1_minute` (integer, required): The maximum requests per minute.
- `max_tokens_per_1_minute` (integer, required): The maximum tokens per minute.
- `max_images_per_1_minute` (integer, optional): The maximum images per minute. Only present for relevant models.
- `max_audio_megabytes_per_1_minute` (integer, optional): The maximum audio megabytes per minute. Only present for relevant models.
- `max_requests_per_1_day` (integer, optional): The maximum requests per day. Only present for relevant models.
- `batch_1_day_max_input_tokens` (integer, optional): The maximum batch input tokens per day. Only present for relevant models.
### 400
Error response for various conditions.
#### application/json
- `error` (object, required)
  - `code` (string | null, required)
  - `message` (string, required)
  - `param` (string | null, required)
  - `type` (string, required)

## Returns
The updated [ProjectRateLimit](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/projects/proj_abc/rate_limits/rl_xxx \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json" \
  -d '{
      "max_requests_per_1_minute": 500
  }'
```
#### Response
```json
{
    "object": "project.rate_limit",
    "id": "rl-ada",
    "model": "ada",
    "max_requests_per_1_minute": 600,
    "max_tokens_per_1_minute": 150000,
    "max_images_per_1_minute": 10
  }
```
