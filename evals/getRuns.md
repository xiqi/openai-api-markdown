# Get eval runs

Source: https://platform.openai.com/docs/api-reference/evals/getRuns

`GET /v1/evals/{eval_id}/runs`

Get a list of runs for an evaluation.

## Parameters
- `eval_id` (path, string, required): The ID of the evaluation to retrieve runs for.
- `after` (query, string, optional): Identifier for the last run from the previous pagination request.
- `limit` (query, integer, optional): Number of runs to retrieve. Default: `20`.
- `order` (query, string, optional): Sort order for runs by timestamp. Use `asc` for ascending order or `desc` for descending order. Defaults to `asc`. Enum: 'asc', 'desc'. Default: `asc`.
- `status` (query, string, optional): Filter runs by status. One of `queued` | `in_progress` | `failed` | `completed` | `canceled`. Enum: 'queued', 'in_progress', 'completed', 'canceled', 'failed'.

## Responses
### 200
A list of runs for the evaluation
#### application/json
- `object` (string, required): The type of this object. It is always set to "list". Enum: 'list'. Default: `list`.
- `data` (array<object>, required): An array of eval run objects.
  - Items:
    - `object` (string, required): The type of the object. Always "eval.run". Enum: 'eval.run'. Default: `eval.run`.
    - `id` (string, required): Unique identifier for the evaluation run.
    - `eval_id` (string, required): The identifier of the associated evaluation.
    - `status` (string, required): The status of the evaluation run.
    - `model` (string, required): The model that is evaluated, if applicable.
    - `name` (string, required): The name of the evaluation run.
    - `created_at` (integer, required): Unix timestamp (in seconds) when the evaluation run was created.
    - `report_url` (string, required): The URL to the rendered evaluation run report on the UI dashboard.
    - `result_counts` (object, required): Counters summarizing the outcomes of the evaluation run.
      - `total` (integer, required): Total number of executed output items.
      - `errored` (integer, required): Number of output items that resulted in an error.
      - `failed` (integer, required): Number of output items that failed to pass the evaluation.
      - `passed` (integer, required): Number of output items that passed the evaluation.
    - `per_model_usage` (array<object>, required): Usage statistics for each model during the evaluation run.
      - Items:
        - `model_name` (string, required): The name of the model.
        - `invocation_count` (integer, required): The number of invocations.
        - `prompt_tokens` (integer, required): The number of prompt tokens used.
        - `completion_tokens` (integer, required): The number of completion tokens generated.
        - `total_tokens` (integer, required): The total number of tokens used.
        - `cached_tokens` (integer, required): The number of tokens retrieved from cache.
    - `per_testing_criteria_results` (array<object>, required): Results per testing criteria applied during the evaluation run.
      - Items:
        - `testing_criteria` (string, required): A description of the testing criteria.
        - `passed` (integer, required): Number of tests passed for this criteria.
        - `failed` (integer, required): Number of tests failed for this criteria.
    - `data_source` (object, required): Information about the run's data source.
      - Variant (object):
        - `type` (string, required): The type of data source. Always `jsonl`. Enum: 'jsonl'. Default: `jsonl`.
        - `source` (object, required): Determines what populates the `item` namespace in the data source.
          - Variant (object):
            - ...
          - Variant (object):
            - ...
      - Variant (object):
        - `type` (string, required): The type of run data source. Always `completions`. Enum: 'completions'. Default: `completions`.
        - `input_messages` (object, optional): Used when sampling from a model. Dictates the structure of the messages passed into the model. Can either be a reference to a prebuilt trajectory (ie, `item.input_trajectory`), or a template with variable references to the `item` namespace.
          - Variant (object):
            - ...
          - Variant (object):
            - ...
        - `sampling_params` (object, optional)
          - ...
        - `model` (string, optional): The name of the model to use for generating completions (e.g. "o3-mini").
        - `source` (object, required): Determines what populates the `item` namespace in this run's data source.
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
      - Variant (object):
        - `type` (string, required): The type of run data source. Always `responses`. Enum: 'responses'. Default: `responses`.
        - `input_messages` (object, optional): Used when sampling from a model. Dictates the structure of the messages passed into the model. Can either be a reference to a prebuilt trajectory (ie, `item.input_trajectory`), or a template with variable references to the `item` namespace.
          - Variant (object):
            - ...
          - Variant (object):
            - ...
        - `sampling_params` (object, optional)
          - ...
        - `model` (string, optional): The name of the model to use for generating completions (e.g. "o3-mini").
        - `source` (object, required): Determines what populates the `item` namespace in this run's data source.
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
    - `metadata` (object | null, required)
    - `error` (object, required): An object representing an error response from the Eval API.
      - `code` (string, required): The error code.
      - `message` (string, required): The error message.
- `first_id` (string, required): The identifier of the first eval run in the data array.
- `last_id` (string, required): The identifier of the last eval run in the data array.
- `has_more` (boolean, required): Indicates whether there are more evals available.

## Returns
A list of [EvalRun](run-object.md) objects matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/evals/egroup_67abd54d9b0081909a86353f6fb9317a/runs \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

runs = client.evals.runs.list("egroup_67abd54d9b0081909a86353f6fb9317a")
print(runs)
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "object": "eval.run",
      "id": "evalrun_67e0c7d31560819090d60c0780591042",
      "eval_id": "eval_67e0c726d560819083f19a957c4c640b",
      "report_url": "https://platform.openai.com/evaluations/eval_67e0c726d560819083f19a957c4c640b",
      "status": "completed",
      "model": "o3-mini",
      "name": "bulk_with_negative_examples_o3-mini",
      "created_at": 1742784467,
      "result_counts": {
        "total": 1,
        "errored": 0,
        "failed": 0,
        "passed": 1
      },
      "per_model_usage": [
        {
          "model_name": "o3-mini",
          "invocation_count": 1,
          "prompt_tokens": 563,
          "completion_tokens": 874,
          "total_tokens": 1437,
          "cached_tokens": 0
        }
      ],
      "per_testing_criteria_results": [
        {
          "testing_criteria": "Push Notification Summary Grader-1808cd0b-eeec-4e0b-a519-337e79f4f5d1",
          "passed": 1,
          "failed": 0
        }
      ],
      "data_source": {
        "type": "completions",
        "source": {
          "type": "file_content",
          "content": [
            {
              "item": {
                "notifications": "\n- New message from Sarah: \"Can you call me later?\"\n- Your package has been delivered!\n- Flash sale: 20% off electronics for the next 2 hours!\n"
              }
            }
          ]
        },
        "input_messages": {
          "type": "template",
          "template": [
            {
              "type": "message",
              "role": "developer",
              "content": {
                "type": "input_text",
                "text": "\n\n\n\nYou are a helpful assistant that takes in an array of push notifications and returns a collapsed summary of them.\nThe push notification will be provided as follows:\n<push_notifications>\n...notificationlist...\n</push_notifications>\n\nYou should return just the summary and nothing else.\n\n\nYou should return a summary that is concise and snappy.\n\n\nHere is an example of a good summary:\n<push_notifications>\n- Traffic alert: Accident reported on Main Street.- Package out for delivery: Expected by 5 PM.- New friend suggestion: Connect with Emma.\n</push_notifications>\n<summary>\nTraffic alert, package expected by 5pm, suggestion for new friend (Emily).\n</summary>\n\n\nHere is an example of a bad summary:\n<push_notifications>\n- Traffic alert: Accident reported on Main Street.- Package out for delivery: Expected by 5 PM.- New friend suggestion: Connect with Emma.\n</push_notifications>\n<summary>\nTraffic alert reported on main street. You have a package that will arrive by 5pm, Emily is a new friend suggested for you.\n</summary>\n"
              }
            },
            {
              "type": "message",
              "role": "user",
              "content": {
                "type": "input_text",
                "text": "<push_notifications>{{item.notifications}}</push_notifications>"
              }
            }
          ]
        },
        "model": "o3-mini",
        "sampling_params": null
      },
      "error": null,
      "metadata": {}
    }
  ],
  "first_id": "evalrun_67e0c7d31560819090d60c0780591042",
  "last_id": "evalrun_67e0c7d31560819090d60c0780591042",
  "has_more": true
}
```
