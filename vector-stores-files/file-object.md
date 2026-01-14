# The vector store file object

Source: https://platform.openai.com/docs/api-reference/vector-stores-files/file-object

A list of files attached to a vector store.

## Properties
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `vector_store.file`. Enum: 'vector_store.file'.
- `usage_bytes` (integer, required): The total vector store usage in bytes. Note that this may be different from the original file size.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the vector store file was created.
- `vector_store_id` (string, required): The ID of the [vector store](../vector-stores/object.md) that the [File](../files/index.md) is attached to.
- `status` (string, required): The status of the vector store file, which can be either `in_progress`, `completed`, `cancelled`, or `failed`. The status `completed` indicates that the vector store file is ready for use. Enum: 'in_progress', 'completed', 'cancelled', 'failed'.
- `last_error` (object | null, required)
  - Variant (object):
    - `code` (string, required): One of `server_error`, `unsupported_file`, or `invalid_file`. Enum: 'server_error', 'unsupported_file', 'invalid_file'.
    - `message` (string, required): A human-readable description of the error.
- `chunking_strategy` (object, optional): The strategy used to chunk the file.
  - Variant (object):
    - `type` (string, required): Always `static`. Enum: 'static'.
    - `static` (object, required)
      - `max_chunk_size_tokens` (integer, required): The maximum number of tokens in each chunk. The default value is `800`. The minimum value is `100` and the maximum value is `4096`.
      - `chunk_overlap_tokens` (integer, required): The number of tokens that overlap between chunks. The default value is `400`.
        
        Note that the overlap must not exceed half of `max_chunk_size_tokens`.
  - Variant (object):
    - `type` (string, required): Always `other`. Enum: 'other'.
- `attributes` (object | null, optional)
