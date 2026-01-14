# The message object

Source: https://platform.openai.com/docs/api-reference/messages/object

Represents a message within a [thread](../threads/index.md).

## Properties
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `thread.message`. Enum: 'thread.message'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the message was created.
- `thread_id` (string, required): The [thread](../threads/index.md) ID that this message belongs to.
- `status` (string, required): The status of the message, which can be either `in_progress`, `incomplete`, or `completed`. Enum: 'in_progress', 'incomplete', 'completed'.
- `incomplete_details` (object | null, required)
  - Variant (object):
    - `reason` (string, required): The reason the message is incomplete. Enum: 'content_filter', 'max_tokens', 'run_cancelled', 'run_expired', 'run_failed'.
- `completed_at` (integer | null, required)
- `incomplete_at` (integer | null, required)
- `role` (string, required): The entity that produced the message. One of `user` or `assistant`. Enum: 'user', 'assistant'.
- `content` (array<object>, required): The content of the message in array of text and/or images.
- `assistant_id` (string | null, required)
- `run_id` (string | null, required)
- `attachments` (array<object> | null, required)
- `metadata` (object | null, required)
