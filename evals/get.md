# Get an eval

Source: https://platform.openai.com/docs/api-reference/evals/get

`GET /v1/evals/{eval_id}`

Get an evaluation by ID.

## Parameters
- `eval_id` (path, string, required): The ID of the evaluation to retrieve.

## Responses
### 200
The evaluation
#### application/json
- `object` (string, required): The object type. Enum: 'eval'. Default: `eval`.
- `id` (string, required): Unique identifier for the evaluation.
- `name` (string, required): The name of the evaluation.
- `data_source_config` (object, required): Configuration of data sources used in runs of the evaluation.
  - Variant (object):
    - `type` (string, required): The type of data source. Always `custom`. Enum: 'custom'. Default: `custom`.
    - `schema` (object, required): The json schema for the run data source items.
      Learn how to build JSON schemas [here](https://json-schema.org/).
  - Variant (object):
    - `type` (string, required): The type of data source. Always `logs`. Enum: 'logs'. Default: `logs`.
    - `metadata` (object | null, optional)
    - `schema` (object, required): The json schema for the run data source items.
      Learn how to build JSON schemas [here](https://json-schema.org/).
  - Variant (object):
    - `type` (string, required): The type of data source. Always `stored_completions`. Enum: 'stored_completions'. Default: `stored_completions`.
    - `metadata` (object | null, optional)
    - `schema` (object, required): The json schema for the run data source items.
      Learn how to build JSON schemas [here](https://json-schema.org/).
- `testing_criteria` (array<object>, required): A list of testing criteria. Default: `eval`.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the eval was created.
- `metadata` (object | null, required)

## Returns
The [Eval](object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/evals/eval_67abd54d9b0081909a86353f6fb9317a \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

eval_obj = client.evals.retrieve("eval_67abd54d9b0081909a86353f6fb9317a")
print(eval_obj)
```
#### Response
```json
{
  "object": "eval",
  "id": "eval_67abd54d9b0081909a86353f6fb9317a",
  "data_source_config": {
    "type": "custom",
    "schema": {
      "type": "object",
      "properties": {
        "item": {
          "type": "object",
          "properties": {
            "input": {
              "type": "string"
            },
            "ground_truth": {
              "type": "string"
            }
          },
          "required": [
            "input",
            "ground_truth"
          ]
        }
      },
      "required": [
        "item"
      ]
    }
  },
  "testing_criteria": [
    {
      "name": "String check",
      "id": "String check-2eaf2d8d-d649-4335-8148-9535a7ca73c2",
      "type": "string_check",
      "input": "{{item.input}}",
      "reference": "{{item.ground_truth}}",
      "operation": "eq"
    }
  ],
  "name": "External Data Eval",
  "created_at": 1739314509,
  "metadata": {},
}
```
