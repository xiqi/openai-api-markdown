# Costs

Source: https://platform.openai.com/docs/api-reference/usage/costs

`GET /v1/organization/costs`

Get costs details for the organization.

## Parameters
- `start_time` (query, integer, required): Start time (Unix seconds) of the query time range, inclusive.
- `end_time` (query, integer, optional): End time (Unix seconds) of the query time range, exclusive.
- `bucket_width` (query, string, optional): Width of each time bucket in response. Currently only `1d` is supported, default to `1d`. Enum: '1d'. Default: `1d`.
- `project_ids` (query, array<string>, optional): Return only costs for these projects.
- `group_by` (query, array<string>, optional): Group the costs by the specified fields. Support fields include `project_id`, `line_item` and any combination of them.
- `limit` (query, integer, optional): A limit on the number of buckets to be returned. Limit can range between 1 and 180, and the default is 7. Default: `7`.
- `page` (query, string, optional): A cursor for use in pagination. Corresponding to the `next_page` field from the previous response.

## Responses
### 200
Costs data retrieved successfully.
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
A list of paginated, time bucketed [Costs](costs_object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl "https://api.openai.com/v1/organization/costs?start_time=1730419200&limit=1" \
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
                    "object": "organization.costs.result",
                    "amount": {
                        "value": 0.06,
                        "currency": "usd"
                    },
                    "line_item": null,
                    "project_id": null
                }
            ]
        }
    ],
    "has_more": false,
    "next_page": null
}
```
