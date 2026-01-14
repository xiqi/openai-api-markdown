# The project service account object

Source: https://platform.openai.com/docs/api-reference/project-service-accounts/object

Represents an individual service account in a project.

## Properties
- `object` (string, required): The object type, which is always `organization.project.service_account` Enum: 'organization.project.service_account'.
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the service account
- `role` (string, required): `owner` or `member` Enum: 'owner', 'member'.
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the service account was created
