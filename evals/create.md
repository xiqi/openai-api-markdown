# Create eval

Source: https://platform.openai.com/docs/api-reference/evals/create

`POST /v1/evals`

Create the structure of an evaluation that can be used to test a model's performance.
An evaluation is a set of testing criteria and the config for a data source, which dictates the schema of the data used in the evaluation. After creating an evaluation, you can run it on different models and model parameters. We support several types of graders and datasources.
For more information, see the [Evals guide](https://platform.openai.com/docs/guides/evals).

## Request body
### application/json
- `name` (string, optional): The name of the evaluation.
- `metadata` (object | null, optional)
- `data_source_config` (object, required): The configuration for the data source used for the evaluation runs. Dictates the schema of the data used in the evaluation.
  - Variant (object):
    - `type` (string, required): The type of data source. Always `custom`. Enum: 'custom'. Default: `custom`.
    - `item_schema` (object, required): The json schema for each row in the data source.
    - `include_sample_schema` (boolean, optional): Whether the eval should expect you to populate the sample namespace (ie, by generating responses off of your data source) Default: `False`.
  - Variant (object):
    - `type` (string, required): The type of data source. Always `logs`. Enum: 'logs'. Default: `logs`.
    - `metadata` (object, optional): Metadata filters for the logs data source.
  - Variant (object):
    - `type` (string, required): The type of data source. Always `stored_completions`. Enum: 'stored_completions'. Default: `stored_completions`.
    - `metadata` (object, optional): Metadata filters for the stored completions data source.
- `testing_criteria` (array<object>, required): A list of graders for all eval runs in this group. Graders can reference variables in the data source using double curly braces notation, like `{{item.variable_name}}`. To reference the model's output, use the `sample` namespace (ie, `{{sample.output_text}}`).

## Responses
### 201
OK
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
The created [Eval](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/evals \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
        "name": "Sentiment",
        "data_source_config": {
          "type": "stored_completions",
          "metadata": {
              "usecase": "chatbot"
          }
        },
        "testing_criteria": [
          {
            "type": "label_model",
            "model": "o3-mini",
            "input": [
              {
                "role": "developer",
                "content": "Classify the sentiment of the following statement as one of 'positive', 'neutral', or 'negative'"
              },
              {
                "role": "user",
                "content": "Statement: {{item.input}}"
              }
            ],
            "passing_labels": [
              "positive"
            ],
            "labels": [
              "positive",
              "neutral",
              "negative"
            ],
            "name": "Example label grader"
          }
        ]
      }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

eval_obj = client.evals.create(
  name="Sentiment",
  data_source_config={
    "type": "stored_completions",
    "metadata": {"usecase": "chatbot"}
  },
  testing_criteria=[
    {
      "type": "label_model",
      "model": "o3-mini",
      "input": [
        {"role": "developer", "content": "Classify the sentiment of the following statement as one of 'positive', 'neutral', or 'negative'"},
        {"role": "user", "content": "Statement: {{item.input}}"}
      ],
      "passing_labels": ["positive"],
      "labels": ["positive", "neutral", "negative"],
      "name": "Example label grader"
    }
  ]
)
print(eval_obj)
```
#### Response
```json
{
  "object": "eval",
  "id": "eval_67b7fa9a81a88190ab4aa417e397ea21",
  "data_source_config": {
    "type": "stored_completions",
    "metadata": {
      "usecase": "chatbot"
    },
    "schema": {
      "type": "object",
      "properties": {
        "item": {
          "type": "object"
        },
        "sample": {
          "type": "object"
        }
      },
      "required": [
        "item",
        "sample"
      ]
  },
  "testing_criteria": [
    {
      "name": "Example label grader",
      "type": "label_model",
      "model": "o3-mini",
      "input": [
        {
          "type": "message",
          "role": "developer",
          "content": {
            "type": "input_text",
            "text": "Classify the sentiment of the following statement as one of positive, neutral, or negative"
          }
        },
        {
          "type": "message",
          "role": "user",
          "content": {
            "type": "input_text",
            "text": "Statement: {{item.input}}"
          }
        }
      ],
      "passing_labels": [
        "positive"
      ],
      "labels": [
        "positive",
        "neutral",
        "negative"
      ]
    }
  ],
  "name": "Sentiment",
  "created_at": 1740110490,
  "metadata": {
    "description": "An eval for sentiment analysis"
  }
}
```
