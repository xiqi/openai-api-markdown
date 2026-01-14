# List project API keys

Source: https://platform.openai.com/docs/api-reference/project-api-keys/list

`GET /v1/organization/projects/{project_id}/api_keys`

Returns a list of API keys in the project.

## Parameters
- `project_id` (path, string, required): The ID of the project.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.

## Responses
### 200
Project API keys listed successfully.
#### application/json
- `object` (string, required) Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `object` (string, required): The object type, which is always `organization.project.api_key` Enum: 'organization.project.api_key'.
    - `redacted_value` (string, required): The redacted value of the API key
    - `name` (string, required): The name of the API key
    - `created_at` (integer, required): The Unix timestamp (in seconds) of when the API key was created
    - `last_used_at` (integer, required): The Unix timestamp (in seconds) of when the API key was last used.
    - `id` (string, required): The identifier, which can be referenced in API endpoints
    - `owner` (object, required)
      - `type` (string, optional): `user` or `service_account` Enum: 'user', 'service_account'.
      - `user` (object, optional): Represents an individual user in a project.
        - `object` (string, required): The object type, which is always `organization.project.user` Enum: 'organization.project.user'.
        - `id` (string, required): The identifier, which can be referenced in API endpoints
        - `name` (string, required): The name of the user
        - `email` (string, required): The email address of the user
        - `role` (string, required): `owner` or `member` Enum: 'owner', 'member'.
        - `added_at` (integer, required): The Unix timestamp (in seconds) of when the project was added.
      - `service_account` (object, optional): Represents an individual service account in a project.
        - `object` (string, required): The object type, which is always `organization.project.service_account` Enum: 'organization.project.service_account'.
        - `id` (string, required): The identifier, which can be referenced in API endpoints
        - `name` (string, required): The name of the service account
        - `role` (string, required): `owner` or `member` Enum: 'owner', 'member'.
        - `created_at` (integer, required): The Unix timestamp (in seconds) of when the service account was created
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of [ProjectApiKey](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/projects/proj_abc/api_keys?after=key_abc&limit=20 \
  -H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
  -H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "object": "organization.project.api_key",
            "redacted_value": "sk-abc...def",
            "name": "My API Key",
            "created_at": 1711471533,
            "last_used_at": 1711471534,
            "id": "key_abc",
            "owner": {
                "type": "user",
                "user": {
                    "object": "organization.project.user",
                    "id": "user_abc",
                    "name": "First Last",
                    "email": "user@example.com",
                    "role": "owner",
                    "added_at": 1711471533
                }
            }
        }
    ],
    "first_id": "key_abc",
    "last_id": "key_xyz",
    "has_more": false
}
```
