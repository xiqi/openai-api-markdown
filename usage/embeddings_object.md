# Embeddings usage object

Source: https://platform.openai.com/docs/api-reference/usage/embeddings_object

The aggregated embeddings usage details of the specific time bucket.

## Properties
- `object` (string, required) Enum: 'organization.usage.embeddings.result'.
- `input_tokens` (integer, required): The aggregated number of input tokens used.
- `num_model_requests` (integer, required): The count of requests made to the model.
- `project_id` (string | null, optional)
- `user_id` (string | null, optional)
- `api_key_id` (string | null, optional)
- `model` (string | null, optional)
