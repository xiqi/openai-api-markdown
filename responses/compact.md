# Compact a response

Source: https://platform.openai.com/docs/api-reference/responses/compact

`POST /v1/responses/compact`

Compact conversation

## Request body
### application/json
- `model` (string | null, required): Model ID used to generate the response, like `gpt-5` or `o3`. OpenAI offers a wide range of models with different capabilities, performance characteristics, and price points. Refer to the [model guide](https://platform.openai.com/docs/models) to browse and compare available models.
- `input` (string | array<object> | null, optional)
- `previous_response_id` (string | null, optional)
- `instructions` (string | null, optional)
### application/x-www-form-urlencoded
- `model` (string | null, required): Model ID used to generate the response, like `gpt-5` or `o3`. OpenAI offers a wide range of models with different capabilities, performance characteristics, and price points. Refer to the [model guide](https://platform.openai.com/docs/models) to browse and compare available models.
- `input` (string | array<object> | null, optional)
- `previous_response_id` (string | null, optional)
- `instructions` (string | null, optional)

## Responses
### 200
Success
#### application/json
- `id` (string, required): The unique identifier for the compacted response.
- `object` (string, required): The object type. Always `response.compaction`. Enum: 'response.compaction'. Default: `response.compaction`.
- `output` (array<object>, required): The compacted list of output items.
- `created_at` (integer, required): Unix timestamp (in seconds) when the compacted conversation was created.
- `usage` (object, required): Represents token usage details including input tokens, output tokens,
  a breakdown of output tokens, and the total tokens used.
  - `input_tokens` (integer, required): The number of input tokens.
  - `input_tokens_details` (object, required): A detailed breakdown of the input tokens.
    - `cached_tokens` (integer, required): The number of tokens that were retrieved from the cache. 
      [More on prompt caching](https://platform.openai.com/docs/guides/prompt-caching).
  - `output_tokens` (integer, required): The number of output tokens.
  - `output_tokens_details` (object, required): A detailed breakdown of the output tokens.
    - `reasoning_tokens` (integer, required): The number of reasoning tokens.
  - `total_tokens` (integer, required): The total number of tokens used.

Example:
```json
{
  "id": "resp_001",
  "object": "response.compaction",
  "output": [
    {
      "type": "message",
      "role": "user",
      "content": [
        {
          "type": "input_text",
          "text": "Summarize our launch checklist from last week."
        }
      ]
    },
    {
      "type": "message",
      "role": "user",
      "content": [
        {
          "type": "input_text",
          "text": "You are performing a CONTEXT CHECKPOINT COMPACTION..."
        }
      ]
    },
    {
      "type": "compaction",
      "id": "cmp_001",
      "encrypted_content": "encrypted-summary"
    }
  ],
  "created_at": 1731459200,
  "usage": {
    "input_tokens": 42897,
    "output_tokens": 12000,
    "total_tokens": 54912
  }
}
```

## Returns
A [compacted response object](compacted-object.md).

Learn when and how to compact long-running conversations in the [conversation state guide](https://platform.openai.com/docs/guides/conversation-state#managing-the-context-window).
For ZDR-compatible compaction details, see [Compaction (advanced)](https://platform.openai.com/docs/guides/conversation-state#compaction-advanced).

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/responses/compact \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
      "model": "gpt-5.1-codex-max",
      "input": [
        {
          "role": "user",
          "content": "Create a simple landing page for a dog petting café."
        },
        {
          "id": "msg_001",
          "type": "message",
          "status": "completed",
          "content": [
            {
              "type": "output_text",
              "annotations": [],
              "logprobs": [],
              "text": "Below is a single file, ready-to-use landing page for a dog petting café:..."
            }
          ],
          "role": "assistant"
        }
      ]
    }'
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

compacted_response = client.responses.compact(
    model="gpt-5.1-codex-max",
    input=[
    {
        "role": "user",
        "content": "Create a simple landing page for a dog petting cafe.",
    },
    # All items returned from previous requests are included here, like reasoning, message, function call, etc.
    {
        "id": "msg_001",
        "type": "message",
        "status": "completed",
        "content": [
        {
            "type": "output_text",
            "annotations": [],
            "logprobs": [],
            "text": "Below is a single file, ready-to-use landing page for a dog petting café:...",
        },
        ],
        "role": "assistant",
    },
    ]
)
# Pass the compacted_response.output as input to the next request
print(compacted_response)
```
#### Response
```json
{
  "id": "resp_001",
  "object": "response.compaction",
  "created_at": 1764967971,
  "output": [
    {
      "id": "msg_000",
      "type": "message",
      "status": "completed",
      "content": [
        {
          "type": "input_text",
          "text": "Create a simple landing page for a dog petting cafe."
        }
      ],
      "role": "user"
    },
    {
      "id": "cmp_001",
      "type": "compaction",
      "encrypted_content": "gAAAAABpM0Yj-...="
    }
  ],
  "usage": {
    "input_tokens": 139,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "output_tokens": 438,
    "output_tokens_details": {
      "reasoning_tokens": 64
    },
    "total_tokens": 577
  }
}
```
