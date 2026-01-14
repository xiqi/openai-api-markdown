# The assistant object

Source: https://platform.openai.com/docs/api-reference/assistants/object

Represents an `assistant` that can call the model and use tools.

## Properties
- `id` (string, required): The identifier, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `assistant`. Enum: 'assistant'.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the assistant was created.
- `name` (string | null, required)
- `description` (string | null, required)
- `model` (string, required): ID of the model to use. You can use the [List models](../models/list.md) API to see all of your available models, or see our [Model overview](https://platform.openai.com/docs/models) for descriptions of them.
- `instructions` (string | null, required)
- `tools` (array<object>, required): A list of tool enabled on the assistant. There can be a maximum of 128 tools per assistant. Tools can be of types `code_interpreter`, `file_search`, or `function`. Default: `[]`.
- `tool_resources` (object | null, optional)
  - Variant (object):
    - `code_interpreter` (object, optional)
      - `file_ids` (array<string>, optional): A list of [file](../files/index.md) IDs made available to the `code_interpreter`` tool. There can be a maximum of 20 files associated with the tool. Default: `[]`.
    - `file_search` (object, optional)
      - `vector_store_ids` (array<string>, optional): The ID of the [vector store](../vector-stores/object.md) attached to this assistant. There can be a maximum of 1 vector store attached to the assistant.
- `metadata` (object | null, required)
- `temperature` (number | null, optional)
- `top_p` (number | null, optional)
- `response_format` (string | object | null, optional)
