# The model object

Source: https://platform.openai.com/docs/api-reference/models/object

Describes an OpenAI model offering that can be used with the API.

## Properties
- `id` (string, required): The model identifier, which can be referenced in the API endpoints.
- `created` (integer, required): The Unix timestamp (in seconds) when the model was created.
- `object` (string, required): The object type, which is always "model". Enum: 'model'.
- `owned_by` (string, required): The organization that owns the model.
