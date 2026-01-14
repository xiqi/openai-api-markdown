# Create container

Source: https://platform.openai.com/docs/api-reference/containers/createContainers

`POST /v1/containers`

Create Container

## Request body
### application/json
- `name` (string, required): Name of the container to create.
- `file_ids` (array<string>, optional): IDs of files to copy to the container.
- `expires_after` (object, optional): Container expiration time in seconds relative to the 'anchor' time.
  - `anchor` (string, required): Time anchor for the expiration time. Currently only 'last_active_at' is supported. Enum: 'last_active_at'.
  - `minutes` (integer, required)
- `memory_limit` (string, optional): Optional memory limit for the container. Defaults to "1g". Enum: '1g', '4g', '16g', '64g'.

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
The created [container](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/containers \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
        "name": "My Container",
        "memory_limit": "4g"
      }'
```
#### Response
```json
{
    "id": "cntr_682e30645a488191b6363a0cbefc0f0a025ec61b66250591",
    "object": "container",
    "created_at": 1747857508,
    "status": "running",
    "expires_after": {
        "anchor": "last_active_at",
        "minutes": 20
    },
    "last_active_at": 1747857508,
    "memory_limit": "4g",
    "name": "My Container"
}
```
