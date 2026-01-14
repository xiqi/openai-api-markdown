# Retrieve assistant

Source: https://platform.openai.com/docs/api-reference/assistants/getAssistant

`GET /v1/assistants/{assistant_id}`

Retrieves an assistant.

## Parameters
- `assistant_id` (path, string, required): The ID of the assistant to retrieve.

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
The [assistant](object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/assistants/asst_abc123 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Beta: assistants=v2"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

my_assistant = client.beta.assistants.retrieve("asst_abc123")
print(my_assistant)
```
#### Response
```json
{
  "id": "asst_abc123",
  "object": "assistant",
  "created_at": 1699009709,
  "name": "HR Helper",
  "description": null,
  "model": "gpt-4o",
  "instructions": "You are an HR bot, and you have access to files to answer employee questions about company policies.",
  "tools": [
    {
      "type": "file_search"
    }
  ],
  "metadata": {},
  "top_p": 1.0,
  "temperature": 1.0,
  "response_format": "auto"
}
```
