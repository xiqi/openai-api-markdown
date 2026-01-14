# List container files

Source: https://platform.openai.com/docs/api-reference/container-files/listContainerFiles

`GET /v1/containers/{container_id}/files`

List Container files

## Parameters
- `container_id` (path, string, required)
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `order` (query, string, optional): Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and `desc` for descending order. Enum: 'asc', 'desc'. Default: `desc`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.

## Responses
### 200
Success
#### application/json
- `object` (string, required): The type of object returned, must be 'list'. Enum: 'list'.
- `data` (array<object>, required): A list of container files.
  - Items:
    - `id` (string, required): Unique identifier for the file.
    - `object` (string, required): The type of this object (`container.file`).
    - `container_id` (string, required): The container this file belongs to.
    - `created_at` (integer, required): Unix timestamp (in seconds) when the file was created.
    - `bytes` (integer, required): Size of the file in bytes.
    - `path` (string, required): Path of the file in the container.
    - `source` (string, required): Source of the file (e.g., `user`, `assistant`).
- `first_id` (string, required): The ID of the first file in the list.
- `last_id` (string, required): The ID of the last file in the list.
- `has_more` (boolean, required): Whether there are more files available.

## Returns
a list of [container file](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/containers/cntr_682e0e7318108198aa783fd921ff305e08e78805b9fdbb04/files \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "id": "cfile_682e0e8a43c88191a7978f477a09bdf5",
            "object": "container.file",
            "created_at": 1747848842,
            "bytes": 880,
            "container_id": "cntr_682e0e7318108198aa783fd921ff305e08e78805b9fdbb04",
            "path": "/mnt/data/88e12fa445d32636f190a0b33daed6cb-tsconfig.json",
            "source": "user"
        }
    ],
    "first_id": "cfile_682e0e8a43c88191a7978f477a09bdf5",
    "has_more": false,
    "last_id": "cfile_682e0e8a43c88191a7978f477a09bdf5"
}
```
