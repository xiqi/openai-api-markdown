# Completions usage object

Source: https://platform.openai.com/docs/api-reference/usage/completions_object

The aggregated completions usage details of the specific time bucket.

## Properties
- `object` (string, required) Enum: 'organization.usage.completions.result'.
- `input_tokens` (integer, required): The aggregated number of text input tokens used, including cached tokens. For customers subscribe to scale tier, this includes scale tier tokens.
- `input_cached_tokens` (integer, optional): The aggregated number of text input tokens that has been cached from previous requests. For customers subscribe to scale tier, this includes scale tier tokens.
- `output_tokens` (integer, required): The aggregated number of text output tokens used. For customers subscribe to scale tier, this includes scale tier tokens.
- `input_audio_tokens` (integer, optional): The aggregated number of audio input tokens used, including cached tokens.
- `output_audio_tokens` (integer, optional): The aggregated number of audio output tokens used.
- `num_model_requests` (integer, required): The count of requests made to the model.
- `project_id` (string | null, optional)
- `user_id` (string | null, optional)
- `api_key_id` (string | null, optional)
- `model` (string | null, optional)
- `batch` (boolean | null, optional)
- `service_tier` (string | null, optional)
