# Remix video

Source: https://platform.openai.com/docs/api-reference/videos/remix

`POST /v1/videos/{video_id}/remix`

Create a video remix

## Parameters
- `video_id` (path, string, required): The identifier of the completed video to remix.

## Request body
### multipart/form-data
- `prompt` (string, required): Updated text prompt that directs the remix generation.
### application/json
- `prompt` (string, required): Updated text prompt that directs the remix generation.

## Responses
### 200
Success
#### application/json
- `id` (string, required): Unique identifier for the video job.
- `object` (string, required): The object type, which is always `video`. Enum: 'video'. Default: `video`.
- `model` (string, required): The video generation model that produced the job.
- `status` (string, required): Current lifecycle status of the video job. Enum: 'queued', 'in_progress', 'completed', 'failed'.
- `progress` (integer, required): Approximate completion percentage for the generation task.
- `created_at` (integer, required): Unix timestamp (seconds) for when the job was created.
- `completed_at` (integer | null, required)
- `expires_at` (integer | null, required)
- `prompt` (string | null, required)
- `size` (string, required): The resolution of the generated video. Enum: '720x1280', '1280x720', '1024x1792', '1792x1024'.
- `seconds` (string, required): Duration of the generated clip in seconds. Enum: '4', '8', '12'.
- `remixed_from_video_id` (string | null, required)
- `error` (object | null, required)
  - Variant (object):
    - `code` (string, required): A machine-readable error code that was returned.
    - `message` (string, required): A human-readable description of the error that was returned.

## Returns
Creates a remix of the specified [video job](object.md) using the provided prompt.

## Examples
### Remix a generated video
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/videos/video_123/remix \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Extend the scene with the cat taking a bow to the cheering audience"
  }'
```
#### Request (javascript)
```javascript
import OpenAI from 'openai';

const client = new OpenAI();

const video = await client.videos.remix('video_123', { prompt: 'Extend the scene with the cat taking a bow to the cheering audience' });

console.log(video.id);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
video = client.videos.remix(
    video_id="video_123",
    prompt="Extend the scene with the cat taking a bow to the cheering audience",
)
print(video.id)
```
#### Response
```json
{
  "id": "video_456",
  "object": "video",
  "model": "sora-2",
  "status": "queued",
  "progress": 0,
  "created_at": 1712698600,
  "size": "720x1280",
  "seconds": "8",
  "remixed_from_video_id": "video_123"
}
```
