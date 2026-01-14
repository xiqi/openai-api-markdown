# Get input token counts

Source: https://platform.openai.com/docs/api-reference/responses/input-tokens

`POST /v1/responses/input_tokens`

Get input token counts

## Request body
### application/json
- `model` (string | null, optional)
- `input` (string | array<object> | null, optional)
- `previous_response_id` (string | null, optional)
- `tools` (array<object> | null, optional)
- `text` (object | null, optional)
  - Variant (object):
    - `format` (object, optional): An object specifying the format that the model must output.
      
      Configuring `{ "type": "json_schema" }` enables Structured Outputs, 
      which ensures the model will match your supplied JSON schema. Learn more in the 
      [Structured Outputs guide](https://platform.openai.com/docs/guides/structured-outputs).
      
      The default format is `{ "type": "text" }` with no additional options.
      
      **Not recommended for gpt-4o and newer models:**
      
      Setting to `{ "type": "json_object" }` enables the older JSON mode, which
      ensures the message the model generates is valid JSON. Using `json_schema`
      is preferred for models that support it.
      - Variant (object):
        - `type` (string, required): The type of response format being defined. Always `text`. Enum: 'text'.
      - Variant (object):
        - `type` (string, required): The type of response format being defined. Always `json_schema`. Enum: 'json_schema'.
        - `description` (string, optional): A description of what the response format is for, used by the model to
          determine how to respond in the format.
        - `name` (string, required): The name of the response format. Must be a-z, A-Z, 0-9, or contain
          underscores and dashes, with a maximum length of 64.
        - `schema` (object, required): The schema for the response format, described as a JSON Schema object.
          Learn how to build JSON schemas [here](https://json-schema.org/).
        - `strict` (boolean | null, optional)
      - Variant (object):
        - `type` (string, required): The type of response format being defined. Always `json_object`. Enum: 'json_object'.
    - `verbosity` (string | null, optional)
- `reasoning` (object | null, optional)
  - Variant (object):
    - `effort` (string | null, optional)
    - `summary` (string | null, optional)
    - `generate_summary` (string | null, optional)
- `truncation` (string, optional): The truncation strategy to use for the model response. - `auto`: If the input to this Response exceeds the model's context window size, the model will truncate the response to fit the context window by dropping items from the beginning of the conversation. - `disabled` (default): If the input size will exceed the context window size for a model, the request will fail with a 400 error. Enum: 'auto', 'disabled'.
- `instructions` (string | null, optional)
- `conversation` (string | object | null, optional)
- `tool_choice` (string | object | null, optional)
- `parallel_tool_calls` (boolean | null, optional)
### application/x-www-form-urlencoded
- `model` (string | null, optional)
- `input` (string | array<object> | null, optional)
- `previous_response_id` (string | null, optional)
- `tools` (array<object> | null, optional)
- `text` (object | null, optional)
  - Variant (object):
    - `format` (object, optional): An object specifying the format that the model must output.
      
      Configuring `{ "type": "json_schema" }` enables Structured Outputs, 
      which ensures the model will match your supplied JSON schema. Learn more in the 
      [Structured Outputs guide](https://platform.openai.com/docs/guides/structured-outputs).
      
      The default format is `{ "type": "text" }` with no additional options.
      
      **Not recommended for gpt-4o and newer models:**
      
      Setting to `{ "type": "json_object" }` enables the older JSON mode, which
      ensures the message the model generates is valid JSON. Using `json_schema`
      is preferred for models that support it.
      - Variant (object):
        - `type` (string, required): The type of response format being defined. Always `text`. Enum: 'text'.
      - Variant (object):
        - `type` (string, required): The type of response format being defined. Always `json_schema`. Enum: 'json_schema'.
        - `description` (string, optional): A description of what the response format is for, used by the model to
          determine how to respond in the format.
        - `name` (string, required): The name of the response format. Must be a-z, A-Z, 0-9, or contain
          underscores and dashes, with a maximum length of 64.
        - `schema` (object, required): The schema for the response format, described as a JSON Schema object.
          Learn how to build JSON schemas [here](https://json-schema.org/).
        - `strict` (boolean | null, optional)
      - Variant (object):
        - `type` (string, required): The type of response format being defined. Always `json_object`. Enum: 'json_object'.
    - `verbosity` (string | null, optional)
- `reasoning` (object | null, optional)
  - Variant (object):
    - `effort` (string | null, optional)
    - `summary` (string | null, optional)
    - `generate_summary` (string | null, optional)
- `truncation` (string, optional): The truncation strategy to use for the model response. - `auto`: If the input to this Response exceeds the model's context window size, the model will truncate the response to fit the context window by dropping items from the beginning of the conversation. - `disabled` (default): If the input size will exceed the context window size for a model, the request will fail with a 400 error. Enum: 'auto', 'disabled'.
- `instructions` (string | null, optional)
- `conversation` (string | object | null, optional)
- `tool_choice` (string | object | null, optional)
- `parallel_tool_calls` (boolean | null, optional)

## Responses
### 200
Success
#### application/json
- `object` (string, required) Enum: 'response.input_tokens'. Default: `response.input_tokens`.
- `input_tokens` (integer, required)

Example:
```json
{
  "object": "response.input_tokens",
  "input_tokens": 123
}
```

## Returns
The input token counts.
```json
{
  object: "response.input_tokens"
  input_tokens: 123
}
```

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/responses/input_tokens \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
      "model": "gpt-5",
      "input": "Tell me a joke."
    }'
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

response = client.responses.input_tokens.count(
    model="gpt-5",
    input="Tell me a joke."
)
print(response.input_tokens)
```
#### Response
```json
{
  "object": "response.input_tokens",
  "input_tokens": 11
}
```
