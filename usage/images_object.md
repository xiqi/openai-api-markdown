# Images usage object

Source: https://platform.openai.com/docs/api-reference/usage/images_object

The aggregated images usage details of the specific time bucket.

## Properties
- `object` (string, required) Enum: 'organization.usage.images.result'.
- `images` (integer, required): The number of images processed.
- `num_model_requests` (integer, required): The count of requests made to the model.
- `source` (string | null, optional)
- `size` (string | null, optional)
- `project_id` (string | null, optional)
- `user_id` (string | null, optional)
- `api_key_id` (string | null, optional)
- `model` (string | null, optional)
