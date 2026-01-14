# List evals

Source: https://platform.openai.com/docs/api-reference/evals/list

`GET /v1/evals`

List evaluations for a project.

## Parameters
- `after` (query, string, optional): Identifier for the last eval from the previous pagination request.
- `limit` (query, integer, optional): Number of evals to retrieve. Default: `20`.
- `order` (query, string, optional): Sort order for evals by timestamp. Use `asc` for ascending order or `desc` for descending order. Enum: 'asc', 'desc'. Default: `asc`.
- `order_by` (query, string, optional): Evals can be ordered by creation time or last updated time. Use
  `created_at` for creation time or `updated_at` for last updated time. Enum: 'created_at', 'updated_at'. Default: `created_at`.

## Responses
### 200
A list of evals
#### application/json
- `object` (string, required): The type of this object. It is always set to "list". Enum: 'list'. Default: `list`.
- `data` (array<object>, required): An array of eval objects.
  - Items:
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
- `first_id` (string, required): The identifier of the first eval in the data array.
- `last_id` (string, required): The identifier of the last eval in the data array.
- `has_more` (boolean, required): Indicates whether there are more evals available.

## Returns
A list of [evals](object.md) matching the specified filters.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/evals?limit=1 \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

evals = client.evals.list(limit=1)
print(evals)
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "id": "eval_67abd54d9b0081909a86353f6fb9317a",
      "object": "eval",
      "data_source_config": {
        "type": "stored_completions",
        "metadata": {
          "usecase": "push_notifications_summarizer"
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
        }
      },
      "testing_criteria": [
        {
          "name": "Push Notification Summary Grader",
          "id": "Push Notification Summary Grader-9b876f24-4762-4be9-aff4-db7a9b31c673",
          "type": "label_model",
          "model": "o3-mini",
          "input": [
            {
              "type": "message",
              "role": "developer",
              "content": {
                "type": "input_text",
                "text": "\nLabel the following push notification summary as either correct or incorrect.\nThe push notification and the summary will be provided below.\nA good push notificiation summary is concise and snappy.\nIf it is good, then label it as correct, if not, then incorrect.\n"
              }
            },
            {
              "type": "message",
              "role": "user",
              "content": {
                "type": "input_text",
                "text": "\nPush notifications: {{item.input}}\nSummary: {{sample.output_text}}\n"
              }
            }
          ],
          "passing_labels": [
            "correct"
          ],
          "labels": [
            "correct",
            "incorrect"
          ],
          "sampling_params": null
        }
      ],
      "name": "Push Notification Summary Grader",
      "created_at": 1739314509,
      "metadata": {
        "description": "A stored completions eval for push notification summaries"
      }
    }
  ],
  "first_id": "eval_67abd54d9b0081909a86353f6fb9317a",
  "last_id": "eval_67aa884cf6688190b58f657d4441c8b7",
  "has_more": true
}
```
