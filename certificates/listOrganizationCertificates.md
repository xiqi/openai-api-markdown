# List organization certificates

Source: https://platform.openai.com/docs/api-reference/certificates/listOrganizationCertificates

`GET /v1/organization/certificates`

List uploaded certificates for this organization.

## Parameters
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `order` (query, string, optional): Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and `desc` for descending order. Enum: 'asc', 'desc'. Default: `desc`.

## Responses
### 200
Certificates listed successfully.
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
A list of [Certificate](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/certificates \
-H "Authorization: Bearer $OPENAI_ADMIN_KEY"
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "object": "organization.certificate",
      "id": "cert_abc",
      "name": "My Example Certificate",
      "active": true,
      "created_at": 1234567,
      "certificate_details": {
        "valid_at": 12345667,
        "expires_at": 12345678
      }
    },
  ],
  "first_id": "cert_abc",
  "last_id": "cert_abc",
  "has_more": false
}
```
