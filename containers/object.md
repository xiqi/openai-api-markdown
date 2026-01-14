# The container object

Source: https://platform.openai.com/docs/api-reference/containers/object

## Properties
- `id` (string, required): Unique identifier for the container.
- `object` (string, required): The type of this object.
- `name` (string, required): Name of the container.
- `created_at` (integer, required): Unix timestamp (in seconds) when the container was created.
- `status` (string, required): Status of the container (e.g., active, deleted).
- `last_active_at` (integer, optional): Unix timestamp (in seconds) when the container was last active.
- `expires_after` (object, optional): The container will expire after this time period.
  The anchor is the reference point for the expiration.
  The minutes is the number of minutes after the anchor before the container expires.
  - `anchor` (string, optional): The reference point for the expiration. Enum: 'last_active_at'.
  - `minutes` (integer, optional): The number of minutes after the anchor before the container expires.
- `memory_limit` (string, optional): The memory limit configured for the container. Enum: '1g', '4g', '16g', '64g'.
