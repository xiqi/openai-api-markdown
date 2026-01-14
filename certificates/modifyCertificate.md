# Modify certificate

Source: https://platform.openai.com/docs/api-reference/certificates/modifyCertificate

`POST /v1/organization/certificates/{certificate_id}`

Modify a certificate. Note that only the name can be modified.

## Request body
### application/json
- `name` (string, required): The updated name for the certificate

## Responses
### 200
Certificate modified successfully.
#### application/json
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

## Returns
The updated [Certificate](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/organization/certificates/cert_abc \
-H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
-H "Content-Type: application/json" \
-d '{
  "name": "Renamed Certificate"
}'
```
#### Response
```json
{
  "object": "certificate",
  "id": "cert_abc",
  "name": "Renamed Certificate",
  "created_at": 1234567,
  "certificate_details": {
    "valid_at": 12345667,
    "expires_at": 12345678
  }
}
```
