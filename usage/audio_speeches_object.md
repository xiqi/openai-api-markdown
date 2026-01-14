# Audio speeches usage object

Source: https://platform.openai.com/docs/api-reference/usage/audio_speeches_object

The aggregated audio speeches usage details of the specific time bucket.

## Properties
- `object` (string, required) Enum: 'organization.usage.audio_speeches.result'.
- `characters` (integer, required): The number of characters processed.
- `num_model_requests` (integer, required): The count of requests made to the model.
- `project_id` (string | null, optional)
- `user_id` (string | null, optional)
- `api_key_id` (string | null, optional)
- `model` (string | null, optional)
