# Delete certificate

Source: https://platform.openai.com/docs/api-reference/certificates/deleteCertificate

`DELETE /v1/organization/certificates/{certificate_id}`

Delete a certificate from the organization.

The certificate must be inactive for the organization and all projects.

## Parameters
- `certificate_id` (path, string, required): Unique ID of the certificate to delete.

## Responses
### 200
Certificate deleted successfully.
#### application/json
- `object` (string, required): The object type, must be `certificate.deleted`. Enum: 'certificate.deleted'.
- `id` (string, required): The ID of the certificate that was deleted.

## Returns
A confirmation object indicating the certificate was deleted.

## Examples
### Example
#### Request (curl)
```bash
curl -X DELETE https://api.openai.com/v1/organization/certificates/cert_abc \
-H "Authorization: Bearer $OPENAI_ADMIN_KEY"
```
#### Response
```json
{
  "object": "certificate.deleted",
  "id": "cert_abc"
}
```
