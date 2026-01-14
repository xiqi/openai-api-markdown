# Modify assistant

Source: https://platform.openai.com/docs/api-reference/assistants/modifyAssistant

`POST /v1/assistants/{assistant_id}`

Modifies an assistant.

## Parameters
- `assistant_id` (path, string, required): The ID of the assistant to modify.

## Request body
### application/json
- `model` (string, optional): ID of the model to use. You can use the [List models](../models/list.md) API to see all of your available models, or see our [Model overview](https://platform.openai.com/docs/models) for descriptions of them.
- `reasoning_effort` (string | null, optional)
- `name` (string | null, optional)
- `description` (string | null, optional)
- `instructions` (string | null, optional)
- `tools` (array<object>, optional): A list of tool enabled on the assistant. There can be a maximum of 128 tools per assistant. Tools can be of types `code_interpreter`, `file_search`, or `function`. Default: `[]`.
- `tool_resources` (object | null, optional)
  - Variant (object):
    - `code_interpreter` (object, optional)
      - `file_ids` (array<string>, optional): Overrides the list of [file](../files/index.md) IDs made available to the `code_interpreter` tool. There can be a maximum of 20 files associated with the tool. Default: `[]`.
    - `file_search` (object, optional)
      - `vector_store_ids` (array<string>, optional): Overrides the [vector store](../vector-stores/object.md) attached to this assistant. There can be a maximum of 1 vector store attached to the assistant.
- `metadata` (object | null, optional)
- `temperature` (number | null, optional)
- `top_p` (number | null, optional)
- `response_format` (string | object | null, optional)

## Responses
### 200
OK
#### application/json
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

## Returns
The modified [assistant](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/assistants/asst_abc123 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Beta: assistants=v2" \
  -d '{
      "instructions": "You are an HR bot, and you have access to files to answer employee questions about company policies. Always response with info from either of the files.",
      "tools": [{"type": "file_search"}],
      "model": "gpt-4o"
    }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

my_updated_assistant = client.beta.assistants.update(
  "asst_abc123",
  instructions="You are an HR bot, and you have access to files to answer employee questions about company policies. Always response with info from either of the files.",
  name="HR Helper",
  tools=[{"type": "file_search"}],
  model="gpt-4o"
)

print(my_updated_assistant)
```
#### Response
```json
{
  "id": "asst_123",
  "object": "assistant",
  "created_at": 1699009709,
  "name": "HR Helper",
  "description": null,
  "model": "gpt-4o",
  "instructions": "You are an HR bot, and you have access to files to answer employee questions about company policies. Always response with info from either of the files.",
  "tools": [
    {
      "type": "file_search"
    }
  ],
  "tool_resources": {
    "file_search": {
      "vector_store_ids": []
    }
  },
  "metadata": {},
  "top_p": 1.0,
  "temperature": 1.0,
  "response_format": "auto"
}
```
