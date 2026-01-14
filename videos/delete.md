# Delete video

Source: https://platform.openai.com/docs/api-reference/videos/delete

`DELETE /v1/videos/{video_id}`

Delete a video

## Parameters
- `video_id` (path, string, required): The identifier of the video to delete.

## Responses
### 200
Success
#### application/json
- `object` (string, required): The object type that signals the deletion response. Enum: 'video.deleted'. Default: `video.deleted`.
- `deleted` (boolean, required): Indicates that the video resource was deleted.
- `id` (string, required): Identifier of the deleted video.

## Returns
Returns the deleted video job metadata.

## Examples
### Example
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
video = client.videos.delete(
    "video_123",
)
print(video.id)
```
