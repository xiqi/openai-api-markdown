# Get certificate

Source: https://platform.openai.com/docs/api-reference/certificates/getCertificate

`GET /v1/organization/certificates/{certificate_id}`

Get a certificate that has been uploaded to the organization.

You can get a certificate regardless of whether it is active or not.

## Parameters
- `certificate_id` (path, string, required): Unique ID of the certificate to retrieve.
- `include` (query, array<string>, optional): A list of additional fields to include in the response. Currently the only supported value is `content` to fetch the PEM content of the certificate.

## Responses
### 200
Certificate retrieved successfully.
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
A single [Certificate](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl "https://api.openai.com/v1/organization/certificates/cert_abc?include[]=content" \
-H "Authorization: Bearer $OPENAI_ADMIN_KEY"
```
#### Response
```json
{
  "object": "certificate",
  "id": "cert_abc",
  "name": "My Example Certificate",
  "created_at": 1234567,
  "certificate_details": {
    "valid_at": 1234567,
    "expires_at": 12345678,
    "content": "-----BEGIN CERTIFICATE-----MIIDeT...-----END CERTIFICATE-----"
  }
}
```
