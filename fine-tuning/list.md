# List fine-tuning jobs

Source: https://platform.openai.com/docs/api-reference/fine-tuning/list

`GET /v1/fine_tuning/jobs`

List your organization's fine-tuning jobs

## Parameters
- `after` (query, string, optional): Identifier for the last job from the previous pagination request.
- `limit` (query, integer, optional): Number of fine-tuning jobs to retrieve. Default: `20`.
- `metadata` (query, object, optional): Optional metadata filter. To filter, use the syntax `metadata[k]=v`. Alternatively, set `metadata=null` to indicate no metadata.

## Responses
### 200
OK
#### application/json
- `data` (array<object>, required)
  - Items:
    - `id` (string, required): The object identifier, which can be referenced in the API endpoints.
    - `created_at` (integer, required): The Unix timestamp (in seconds) for when the fine-tuning job was created.
    - `error` (object | null, required)
      - Variant (object):
        - `code` (string, required): A machine-readable error code.
        - `message` (string, required): A human-readable error message.
        - `param` (string | null, required)
    - `fine_tuned_model` (string | null, required)
    - `finished_at` (integer | null, required)
    - `hyperparameters` (object, required): The hyperparameters used for the fine-tuning job. This value will only be returned when running `supervised` jobs.
      - `batch_size` (string | integer | null, optional)
      - `learning_rate_multiplier` (string | number, optional): Scaling factor for the learning rate. A smaller learning rate may be useful to avoid
        overfitting. Default: `auto`.
      - `n_epochs` (string | integer, optional): The number of epochs to train the model for. An epoch refers to one full cycle
        through the training dataset. Default: `auto`.
    - `model` (string, required): The base model that is being fine-tuned.
    - `object` (string, required): The object type, which is always "fine_tuning.job". Enum: 'fine_tuning.job'.
    - `organization_id` (string, required): The organization that owns the fine-tuning job.
    - `result_files` (array<string>, required): The compiled results file ID(s) for the fine-tuning job. You can retrieve the results with the [Files API](../files/retrieve-contents.md).
    - `status` (string, required): The current status of the fine-tuning job, which can be either `validating_files`, `queued`, `running`, `succeeded`, `failed`, or `cancelled`. Enum: 'validating_files', 'queued', 'running', 'succeeded', 'failed', 'cancelled'.
    - `trained_tokens` (integer | null, required)
    - `training_file` (string, required): The file ID used for training. You can retrieve the training data with the [Files API](../files/retrieve-contents.md).
    - `validation_file` (string | null, required)
    - `integrations` (array<object> | null, optional)
    - `seed` (integer, required): The seed used for the fine-tuning job.
    - `estimated_finish` (integer | null, optional)
    - `method` (object, optional): The method used for fine-tuning.
      - `type` (string, required): The type of method. Is either `supervised`, `dpo`, or `reinforcement`. Enum: 'supervised', 'dpo', 'reinforcement'.
      - `supervised` (object, optional): Configuration for the supervised fine-tuning method.
        - `hyperparameters` (object, optional): The hyperparameters used for the fine-tuning job.
          - ...
      - `dpo` (object, optional): Configuration for the DPO fine-tuning method.
        - `hyperparameters` (object, optional): The hyperparameters used for the DPO fine-tuning job.
          - ...
      - `reinforcement` (object, optional): Configuration for the reinforcement fine-tuning method.
        - `grader` (object, required): The grader used for the fine-tuning job.
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
        - `hyperparameters` (object, optional): The hyperparameters used for the reinforcement fine-tuning job.
          - ...
    - `metadata` (object | null, optional)
- `has_more` (boolean, required)
- `object` (string, required) Enum: 'list'.

## Returns
A list of paginated [fine-tuning job](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/fine_tuning/jobs?limit=2&metadata[key]=value \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.fine_tuning.jobs.list()
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "object": "fine_tuning.job",
      "id": "ftjob-abc123",
      "model": "gpt-4o-mini-2024-07-18",
      "created_at": 1721764800,
      "fine_tuned_model": null,
      "organization_id": "org-123",
      "result_files": [],
      "status": "queued",
      "validation_file": null,
      "training_file": "file-abc123",
      "metadata": {
        "key": "value"
      }
    },
    { ... },
    { ... }
  ], "has_more": true
}
```
