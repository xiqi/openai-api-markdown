# List groups

Source: https://platform.openai.com/docs/api-reference/groups/list

`GET /v1/organization/groups`

Lists all groups in the organization.

## Parameters
- `limit` (query, integer, optional): A limit on the number of groups to be returned. Limit can range between 0 and 1000, and the default is 100. Default: `100`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is a group ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with group_abc, your subsequent call can include `after=group_abc` in order to fetch the next page of the list.
- `order` (query, string, optional): Specifies the sort order of the returned groups. Enum: 'asc', 'desc'. Default: `asc`.

## Responses
### 200
Groups listed successfully.
#### application/json
- `object` (string, required): Always `list`. Enum: 'list'.
- `data` (array<object>, required): Groups returned in the current page.
  - Items:
    - `id` (string, required): Identifier for the group.
    - `name` (string, required): Display name of the group.
    - `created_at` (integer, required): Unix timestamp (in seconds) when the group was created.
    - `is_scim_managed` (boolean, required): Whether the group is managed through SCIM and controlled by your identity provider.
- `has_more` (boolean, required): Whether additional groups are available when paginating.
- `next` (string | null, required): Cursor to fetch the next page of results, or `null` if there are no more results.

## Returns
A list of [group objects](object.md).

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/groups?limit=20&order=asc \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "object": "group",
            "id": "group_01J1F8ABCDXYZ",
            "name": "Support Team",
            "created_at": 1711471533,
            "is_scim_managed": false
        }
    ],
    "has_more": false,
    "next": null
}
```
