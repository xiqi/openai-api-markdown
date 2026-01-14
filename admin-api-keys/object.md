# The admin API key object

Source: https://platform.openai.com/docs/api-reference/admin-api-keys/object

Represents an individual Admin API key in an org.

## Properties
- `object` (string, required): The object type, which is always `organization.admin_api_key`
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the API key
- `redacted_value` (string, required): The redacted value of the API key
- `value` (string, optional): The value of the API key. Only shown on create.
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the API key was created
- `last_used_at` (integer | null, required)
- `owner` (object, required)
  - `type` (string, optional): Always `user`
  - `object` (string, optional): The object type, which is always organization.user
  - `id` (string, optional): The identifier, which can be referenced in API endpoints
  - `name` (string, optional): The name of the user
  - `created_at` (integer, optional): The Unix timestamp (in seconds) of when the user was created
  - `role` (string, optional): Always `owner`
