# Vector stores usage object

Source: https://platform.openai.com/docs/api-reference/usage/vector_stores_object

The aggregated vector stores usage details of the specific time bucket.

## Properties
- `object` (string, required) Enum: 'organization.usage.vector_stores.result'.
- `usage_bytes` (integer, required): The vector stores usage in bytes.
- `project_id` (string | null, optional)
