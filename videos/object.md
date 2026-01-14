# Video job

Source: https://platform.openai.com/docs/api-reference/videos/object

Structured information describing a generated video job.

## Properties
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
