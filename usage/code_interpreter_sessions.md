# Code interpreter sessions

Source: https://platform.openai.com/docs/api-reference/usage/code_interpreter_sessions

`GET /v1/organization/usage/code_interpreter_sessions`

Get code interpreter sessions usage details for the organization.

## Parameters
- `start_time` (query, integer, required): Start time (Unix seconds) of the query time range, inclusive.
- `end_time` (query, integer, optional): End time (Unix seconds) of the query time range, exclusive.
- `bucket_width` (query, string, optional): Width of each time bucket in response. Currently `1m`, `1h` and `1d` are supported, default to `1d`. Enum: '1m', '1h', '1d'. Default: `1d`.
- `project_ids` (query, array<string>, optional): Return only usage for these projects.
- `group_by` (query, array<string>, optional): Group the usage data by the specified fields. Support fields include `project_id`.
- `limit` (query, integer, optional): Specifies the number of buckets to return.
  - `bucket_width=1d`: default: 7, max: 31
  - `bucket_width=1h`: default: 24, max: 168
  - `bucket_width=1m`: default: 60, max: 1440
- `page` (query, string, optional): A cursor for use in pagination. Corresponding to the `next_page` field from the previous response.

## Responses
### 200
Usage data retrieved successfully.
#### application/json
- `object` (string, required) Enum: 'page'.
- `data` (array<object>, required)
  - Items:
    - `object` (string, required) Enum: 'bucket'.
    - `start_time` (integer, required)
    - `end_time` (integer, required)
    - `result` (array<object>, required)
- `has_more` (boolean, required)
- `next_page` (string, required)

## Returns
A list of paginated, time bucketed [Code interpreter sessions usage](code_interpreter_sessions_object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl "https://api.openai.com/v1/organization/usage/code_interpreter_sessions?start_time=1730419200&limit=1" \
-H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
-H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "page",
    "data": [
        {
            "object": "bucket",
            "start_time": 1730419200,
            "end_time": 1730505600,
            "results": [
                {
                    "object": "organization.usage.code_interpreter_sessions.result",
                    "num_sessions": 1,
                    "project_id": null
                }
            ]
        }
    ],
    "has_more": false,
    "next_page": null
}
```
