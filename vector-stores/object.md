# The vector store object

Source: https://platform.openai.com/docs/api-reference/vector-stores/object

A vector store is a collection of processed files can be used by the `file_search` tool.

## Properties
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `vector_store`. Enum: 'vector_store'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the vector store was created.
- `name` (string, required): The name of the vector store.
- `usage_bytes` (integer, required): The total number of bytes used by the files in the vector store.
- `file_counts` (object, required)
  - `in_progress` (integer, required): The number of files that are currently being processed.
  - `completed` (integer, required): The number of files that have been successfully processed.
  - `failed` (integer, required): The number of files that have failed to process.
  - `cancelled` (integer, required): The number of files that were cancelled.
  - `total` (integer, required): The total number of files.
- `status` (string, required): The status of the vector store, which can be either `expired`, `in_progress`, or `completed`. A status of `completed` indicates that the vector store is ready for use. Enum: 'expired', 'in_progress', 'completed'.
- `expires_after` (object, optional): The expiration policy for a vector store.
  - `anchor` (string, required): Anchor timestamp after which the expiration policy applies. Supported anchors: `last_active_at`. Enum: 'last_active_at'.
  - `days` (integer, required): The number of days after the anchor time that the vector store will expire.
- `expires_at` (integer | null, optional)
- `last_active_at` (integer | null, required)
- `metadata` (object | null, required)
