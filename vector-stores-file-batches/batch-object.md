# The vector store files batch object

Source: https://platform.openai.com/docs/api-reference/vector-stores-file-batches/batch-object

A batch of files attached to a vector store.

## Properties
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `vector_store.file_batch`. Enum: 'vector_store.files_batch'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the vector store files batch was created.
- `vector_store_id` (string, required): The ID of the [vector store](../vector-stores/object.md) that the [File](../files/index.md) is attached to.
- `status` (string, required): The status of the vector store files batch, which can be either `in_progress`, `completed`, `cancelled` or `failed`. Enum: 'in_progress', 'completed', 'cancelled', 'failed'.
- `file_counts` (object, required)
  - `in_progress` (integer, required): The number of files that are currently being processed.
  - `completed` (integer, required): The number of files that have been processed.
  - `failed` (integer, required): The number of files that have failed to process.
  - `cancelled` (integer, required): The number of files that where cancelled.
  - `total` (integer, required): The total number of files.
