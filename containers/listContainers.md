# List containers

Source: https://platform.openai.com/docs/api-reference/containers/listContainers

`GET /v1/containers`

List Containers

## Parameters
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `order` (query, string, optional): Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and `desc` for descending order. Enum: 'asc', 'desc'. Default: `desc`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.

## Responses
### 200
Success
#### application/json
- `object` (string, required): The type of object returned, must be 'list'. Enum: 'list'.
- `data` (array<object>, required): A list of containers.
  - Items:
    - `id` (string, required): Unique identifier for the container.
    - `object` (string, required): The type of this object.
    - `name` (string, required): Name of the container.
    - `created_at` (integer, required): Unix timestamp (in seconds) when the container was created.
    - `status` (string, required): Status of the container (e.g., active, deleted).
    - `last_active_at` (integer, optional): Unix timestamp (in seconds) when the container was last active.
    - `expires_after` (object, optional): The container will expire after this time period.
      The anchor is the reference point for the expiration.
      The minutes is the number of minutes after the anchor before the container expires.
      - `anchor` (string, optional): The reference point for the expiration. Enum: 'last_active_at'.
      - `minutes` (integer, optional): The number of minutes after the anchor before the container expires.
    - `memory_limit` (string, optional): The memory limit configured for the container. Enum: '1g', '4g', '16g', '64g'.
- `first_id` (string, required): The ID of the first container in the list.
- `last_id` (string, required): The ID of the last container in the list.
- `has_more` (boolean, required): Whether there are more containers available.

## Returns
a list of [container](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/containers \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
        "id": "cntr_682dfebaacac8198bbfe9c2474fb6f4a085685cbe3cb5863",
        "object": "container",
        "created_at": 1747844794,
        "status": "running",
        "expires_after": {
            "anchor": "last_active_at",
            "minutes": 20
        },
        "last_active_at": 1747844794,
        "memory_limit": "4g",
        "name": "My Container"
    }
  ],
  "first_id": "container_123",
  "last_id": "container_123",
  "has_more": false
}
```
