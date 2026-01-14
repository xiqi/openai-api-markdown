# Delete a container

Source: https://platform.openai.com/docs/api-reference/containers/deleteContainer

`DELETE /v1/containers/{container_id}`

Delete Container

## Parameters
- `container_id` (path, string, required): The ID of the container to delete.

## Responses
### 200
OK

## Returns
Deletion Status

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/containers/cntr_682dfebaacac8198bbfe9c2474fb6f4a085685cbe3cb5863 \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
{
    "id": "cntr_682dfebaacac8198bbfe9c2474fb6f4a085685cbe3cb5863",
    "object": "container.deleted",
    "deleted": true
}
```
