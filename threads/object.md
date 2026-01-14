# The thread object

Source: https://platform.openai.com/docs/api-reference/threads/object

Represents a thread that contains [messages](../messages/index.md).

## Properties
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `thread`. Enum: 'thread'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the thread was created.
- `tool_resources` (object | null, required)
  - Variant (object):
    - `code_interpreter` (object, optional)
      - `file_ids` (array<string>, optional): A list of [file](../files/index.md) IDs made available to the `code_interpreter` tool. There can be a maximum of 20 files associated with the tool. Default: `[]`.
    - `file_search` (object, optional)
      - `vector_store_ids` (array<string>, optional): The [vector store](../vector-stores/object.md) attached to this thread. There can be a maximum of 1 vector store attached to the thread.
- `metadata` (object | null, required)
