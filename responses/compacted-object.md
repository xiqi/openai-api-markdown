# The compacted response object

Source: https://platform.openai.com/docs/api-reference/responses/compacted-object

## Properties
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

## Example
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
