# Create video

Source: https://platform.openai.com/docs/api-reference/videos/create

`POST /v1/videos`

Create a video

## Request body
### multipart/form-data
- `model` (string, optional): The video generation model to use (allowed values: sora-2, sora-2-pro). Defaults to `sora-2`.
- `prompt` (string, required): Text prompt that describes the video to generate.
- `input_reference` (string, optional): Optional image reference that guides generation.
- `seconds` (string, optional): Clip duration in seconds (allowed values: 4, 8, 12). Defaults to 4 seconds. Enum: '4', '8', '12'.
- `size` (string, optional): Output resolution formatted as width x height (allowed values: 720x1280, 1280x720, 1024x1792, 1792x1024). Defaults to 720x1280. Enum: '720x1280', '1280x720', '1024x1792', '1792x1024'.
### application/json
- `model` (string, optional): The video generation model to use (allowed values: sora-2, sora-2-pro). Defaults to `sora-2`.
- `prompt` (string, required): Text prompt that describes the video to generate.
- `input_reference` (string, optional): Optional image reference that guides generation.
- `seconds` (string, optional): Clip duration in seconds (allowed values: 4, 8, 12). Defaults to 4 seconds. Enum: '4', '8', '12'.
- `size` (string, optional): Output resolution formatted as width x height (allowed values: 720x1280, 1280x720, 1024x1792, 1792x1024). Defaults to 720x1280. Enum: '720x1280', '1280x720', '1024x1792', '1792x1024'.

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
Returns the newly created [video job](object.md).

## Examples
### Create a video render
#### Request (curl)
```bash
curl https://api.openai.com/v1/videos \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F "model=sora-2" \
  -F "prompt=A calico cat playing a piano on stage"
```
#### Request (javascript)
```javascript
import OpenAI from 'openai';

const openai = new OpenAI();

const video = await openai.videos.create({ prompt: 'A calico cat playing a piano on stage' });

console.log(video.id);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
video = client.videos.create(
    prompt="A calico cat playing a piano on stage",
)
print(video.id)
```
#### Response
```json
{
  "id": "video_123",
  "object": "video",
  "model": "sora-2",
  "status": "queued",
  "progress": 0,
  "created_at": 1712697600,
  "size": "1024x1792",
  "seconds": "8",
  "quality": "standard"
}
```
