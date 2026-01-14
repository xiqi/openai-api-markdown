# List videos

Source: https://platform.openai.com/docs/api-reference/videos/list

`GET /v1/videos`

List videos

## Parameters
- `limit` (query, integer, optional): Number of items to retrieve
- `order` (query, string, optional): Sort order of results by timestamp. Use `asc` for ascending order or `desc` for descending order. Enum: 'asc', 'desc'.
- `after` (query, string, optional): Identifier for the last item from the previous pagination request

## Responses
### 200
Success
#### application/json
- `object` (string, required): The type of object returned, must be `list`. Enum: 'list'. Default: `list`.
- `data` (array<object>, required): A list of items
  - Items:
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
- `first_id` (string | null, required)
- `last_id` (string | null, required)
- `has_more` (boolean, required): Whether there are more items available.

## Returns
Returns a paginated list of [video jobs](object.md) for the organization.

## Examples
### List recent videos
#### Request (curl)
```bash
curl https://api.openai.com/v1/videos \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from 'openai';

const openai = new OpenAI();

// Automatically fetches more pages as needed.
for await (const video of openai.videos.list()) {
  console.log(video.id);
}
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
page = client.videos.list()
page = page.data[0]
print(page.id)
```
#### Response
```json
{
  "data": [
    {
      "id": "video_123",
      "object": "video",
      "model": "sora-2",
      "status": "completed"
    }
  ],
  "object": "list"
}
```
