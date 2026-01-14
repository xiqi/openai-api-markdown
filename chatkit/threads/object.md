# The thread object

Source: https://platform.openai.com/docs/api-reference/chatkit/threads/object

Represents a ChatKit thread and its current status.

## Properties
- `id` (string, required): Identifier of the thread.
- `object` (string, required): Type discriminator that is always `chatkit.thread`. Enum: 'chatkit.thread'. Default: `chatkit.thread`.
- `created_at` (integer, required): Unix timestamp (in seconds) for when the thread was created.
- `title` (string | null, required)
- `status` (object, required): Current status for the thread. Defaults to `active` for newly created threads.
  - Variant (object):
    - `type` (string, required): Status discriminator that is always `active`. Enum: 'active'. Default: `active`.
  - Variant (object):
    - `type` (string, required): Status discriminator that is always `locked`. Enum: 'locked'. Default: `locked`.
    - `reason` (string | null, required)
  - Variant (object):
    - `type` (string, required): Status discriminator that is always `closed`. Enum: 'closed'. Default: `closed`.
    - `reason` (string | null, required)
- `user` (string, required): Free-form string that identifies your end user who owns the thread.

## Example
```json
{
  "id": "cthr_def456",
  "object": "chatkit.thread",
  "created_at": 1712345600,
  "title": "Demo feedback",
  "status": {
    "type": "active"
  },
  "user": "user_456"
}
```
