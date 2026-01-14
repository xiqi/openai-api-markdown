# The invite object

Source: https://platform.openai.com/docs/api-reference/invite/object

Represents an individual `invite` to the organization.

## Properties
- `object` (string, required): The object type, which is always `organization.invite` Enum: 'organization.invite'.
- `id` (string, required): The identifier, which can be referenced in API endpoints
- `email` (string, required): The email address of the individual to whom the invite was sent
- `role` (string, required): `owner` or `reader` Enum: 'owner', 'reader'.
- `status` (string, required): `accepted`,`expired`, or `pending` Enum: 'accepted', 'expired', 'pending'.
- `invited_at` (integer, required): The Unix timestamp (in seconds) of when the invite was sent.
- `expires_at` (integer, required): The Unix timestamp (in seconds) of when the invite expires.
- `accepted_at` (integer, optional): The Unix timestamp (in seconds) of when the invite was accepted.
- `projects` (array<object>, optional): The projects that were granted membership upon acceptance of the invite.
  - Items:
    - `id` (string, optional): Project's public ID
    - `role` (string, optional): Project membership role Enum: 'member', 'owner'.
