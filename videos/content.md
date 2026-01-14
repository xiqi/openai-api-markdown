# Retrieve video content

Source: https://platform.openai.com/docs/api-reference/videos/content

`GET /v1/videos/{video_id}/content`

Download video content

## Parameters
- `video_id` (path, string, required): The identifier of the video whose media to download.
- `variant` (query, string, optional): Which downloadable asset to return. Defaults to the MP4 video. Enum: 'video', 'thumbnail', 'spritesheet'.

## Responses
### 200
The video bytes or preview asset that matches the requested variant.
#### video/mp4
- Schema type: `string`
#### image/webp
- Schema type: `string`
#### application/json
- Schema type: `string`

## Returns
Streams the rendered video content for the specified video job.

## Examples
### Example
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
response = client.videos.download_content(
    video_id="video_123",
)
print(response)
content = response.read()
print(content)
```
