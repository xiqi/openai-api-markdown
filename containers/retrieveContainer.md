# Retrieve container

Source: https://platform.openai.com/docs/api-reference/containers/retrieveContainer

`GET /v1/containers/{container_id}`

Retrieve Container

## Parameters
- `container_id` (path, string, required)

## Responses
### 200
Success
#### application/json
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

## Returns
The [container](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/containers/cntr_682dfebaacac8198bbfe9c2474fb6f4a085685cbe3cb5863 \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
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
```
