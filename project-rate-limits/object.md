# The project rate limit object

Source: https://platform.openai.com/docs/api-reference/project-rate-limits/object

Represents a project rate limit config.

## Properties
- `object` (string, required): The object type, which is always `project.rate_limit` Enum: 'project.rate_limit'.
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `model` (string, required): The model this rate limit applies to.
- `max_requests_per_1_minute` (integer, required): The maximum requests per minute.
- `max_tokens_per_1_minute` (integer, required): The maximum tokens per minute.
- `max_images_per_1_minute` (integer, optional): The maximum images per minute. Only present for relevant models.
- `max_audio_megabytes_per_1_minute` (integer, optional): The maximum audio megabytes per minute. Only present for relevant models.
- `max_requests_per_1_day` (integer, optional): The maximum requests per day. Only present for relevant models.
- `batch_1_day_max_input_tokens` (integer, optional): The maximum batch input tokens per day. Only present for relevant models.
