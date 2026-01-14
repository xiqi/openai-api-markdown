# The certificate object

Source: https://platform.openai.com/docs/api-reference/certificates/object

Represents an individual `certificate` uploaded to the organization.

## Properties
- `object` (string, required): The object type.
  
  - If creating, updating, or getting a specific certificate, the object type is `certificate`.
  - If listing, activating, or deactivating certificates for the organization, the object type is `organization.certificate`.
  - If listing, activating, or deactivating certificates for a project, the object type is `organization.project.certificate`. Enum: 'certificate', 'organization.certificate', 'organization.project.certificate'.
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `name` (string, required): The name of the certificate.
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the certificate was uploaded.
- `certificate_details` (object, required)
  - `valid_at` (integer, optional): The Unix timestamp (in seconds) of when the certificate becomes valid.
  - `expires_at` (integer, optional): The Unix timestamp (in seconds) of when the certificate expires.
  - `content` (string, optional): The content of the certificate in PEM format.
- `active` (boolean, optional): Whether the certificate is currently active at the specified scope. Not returned when getting details for a specific certificate.
