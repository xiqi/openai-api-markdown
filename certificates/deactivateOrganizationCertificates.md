# Deactivate certificates for organization

Source: https://platform.openai.com/docs/api-reference/certificates/deactivateOrganizationCertificates

`POST /v1/organization/certificates/deactivate`

Deactivate certificates at the organization level.

You can atomically and idempotently deactivate up to 10 certificates at a time.

## Request body
### application/json
- `certificate_ids` (array<string>, required)

## Responses
### 200
Certificates deactivated successfully.
#### application/json
- `data` (array<object>, required)
  - Items:
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
- `first_id` (string, optional)
- `last_id` (string, optional)
- `has_more` (boolean, required)
- `object` (string, required) Enum: 'list'.

## Returns
A list of [Certificate](object.md) objects that were deactivated.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/certificates/deactivate \
-H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
-H "Content-Type: application/json" \
-d '{
  "data": ["cert_abc", "cert_def"]
}'
```
#### Response
```json
{
  "object": "organization.certificate.deactivation",
  "data": [
    {
      "object": "organization.certificate",
      "id": "cert_abc",
      "name": "My Example Certificate",
      "active": false,
      "created_at": 1234567,
      "certificate_details": {
        "valid_at": 12345667,
        "expires_at": 12345678
      }
    },
    {
      "object": "organization.certificate",
      "id": "cert_def",
      "name": "My Example Certificate 2",
      "active": false,
      "created_at": 1234567,
      "certificate_details": {
        "valid_at": 12345667,
        "expires_at": 12345678
      }
    },
  ],
}
```
