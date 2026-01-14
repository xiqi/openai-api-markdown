# Resume fine-tuning

Source: https://platform.openai.com/docs/api-reference/fine-tuning/resume

`POST /v1/fine_tuning/jobs/{fine_tuning_job_id}/resume`

Resume a fine-tune job.

## Parameters
- `fine_tuning_job_id` (path, string, required): The ID of the fine-tuning job to resume.

## Responses
### 200
OK
#### application/json
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
      - `batch_size` (string | integer, optional): Number of examples in each batch. A larger batch size means that model parameters are updated less frequently, but with lower variance. Default: `auto`.
      - `learning_rate_multiplier` (string | number, optional): Scaling factor for the learning rate. A smaller learning rate may be useful to avoid overfitting. Default: `auto`.
      - `n_epochs` (string | integer, optional): The number of epochs to train the model for. An epoch refers to one full cycle through the training dataset. Default: `auto`.
  - `dpo` (object, optional): Configuration for the DPO fine-tuning method.
    - `hyperparameters` (object, optional): The hyperparameters used for the DPO fine-tuning job.
      - `beta` (string | number, optional): The beta value for the DPO method. A higher beta value will increase the weight of the penalty between the policy and reference model. Default: `auto`.
      - `batch_size` (string | integer, optional): Number of examples in each batch. A larger batch size means that model parameters are updated less frequently, but with lower variance. Default: `auto`.
      - `learning_rate_multiplier` (string | number, optional): Scaling factor for the learning rate. A smaller learning rate may be useful to avoid overfitting. Default: `auto`.
      - `n_epochs` (string | integer, optional): The number of epochs to train the model for. An epoch refers to one full cycle through the training dataset. Default: `auto`.
  - `reinforcement` (object, optional): Configuration for the reinforcement fine-tuning method.
    - `grader` (object, required): The grader used for the fine-tuning job.
      - Variant (object):
        - `type` (string, required): The object type, which is always `string_check`. Enum: 'string_check'.
        - `name` (string, required): The name of the grader.
        - `input` (string, required): The input text. This may include template strings.
        - `reference` (string, required): The reference text. This may include template strings.
        - `operation` (string, required): The string check operation to perform. One of `eq`, `ne`, `like`, or `ilike`. Enum: 'eq', 'ne', 'like', 'ilike'.
      - Variant (object):
        - `type` (string, required): The type of grader. Enum: 'text_similarity'. Default: `text_similarity`.
        - `name` (string, required): The name of the grader.
        - `input` (string, required): The text being graded.
        - `reference` (string, required): The text being graded against.
        - `evaluation_metric` (string, required): The evaluation metric to use. One of `cosine`, `fuzzy_match`, `bleu`, 
          `gleu`, `meteor`, `rouge_1`, `rouge_2`, `rouge_3`, `rouge_4`, `rouge_5`, 
          or `rouge_l`. Enum: 'cosine', 'fuzzy_match', 'bleu', 'gleu', 'meteor', 'rouge_1', 'rouge_2', 'rouge_3', 'rouge_4', 'rouge_5', 'rouge_l'.
      - Variant (object):
        - `type` (string, required): The object type, which is always `python`. Enum: 'python'.
        - `name` (string, required): The name of the grader.
        - `source` (string, required): The source code of the python script.
        - `image_tag` (string, optional): The image tag to use for the python script.
      - Variant (object):
        - `type` (string, required): The object type, which is always `score_model`. Enum: 'score_model'.
        - `name` (string, required): The name of the grader.
        - `model` (string, required): The model to use for the evaluation.
        - `sampling_params` (object, optional): The sampling parameters for the model.
          - ...
        - `input` (array<object>, required): The input messages evaluated by the grader. Supports text, output text, input image, and input audio content blocks, and may include template strings.
          - Items:
            - ...
        - `range` (array<number>, optional): The range of the score. Defaults to `[0, 1]`.
      - Variant (object):
        - `type` (string, required): The object type, which is always `multi`. Enum: 'multi'. Default: `multi`.
        - `name` (string, required): The name of the grader.
        - `graders` (object, required)
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
        - `calculate_output` (string, required): A formula to calculate the output based on grader results.
    - `hyperparameters` (object, optional): The hyperparameters used for the reinforcement fine-tuning job.
      - `batch_size` (string | integer, optional): Number of examples in each batch. A larger batch size means that model parameters are updated less frequently, but with lower variance. Default: `auto`.
      - `learning_rate_multiplier` (string | number, optional): Scaling factor for the learning rate. A smaller learning rate may be useful to avoid overfitting. Default: `auto`.
      - `n_epochs` (string | integer, optional): The number of epochs to train the model for. An epoch refers to one full cycle through the training dataset. Default: `auto`.
      - `reasoning_effort` (string, optional): Level of reasoning effort. Enum: 'default', 'low', 'medium', 'high'. Default: `default`.
      - `compute_multiplier` (string | number, optional): Multiplier on amount of compute used for exploring search space during training. Default: `auto`.
      - `eval_interval` (string | integer, optional): The number of training steps between evaluation runs. Default: `auto`.
      - `eval_samples` (string | integer, optional): Number of evaluation samples to generate per training step. Default: `auto`.
- `metadata` (object | null, optional)

## Returns
The resumed [fine-tuning](object.md) object.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/fine_tuning/jobs/ftjob-abc123/resume \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.fine_tuning.jobs.resume("ftjob-abc123")
```
#### Response
```json
{
  "object": "fine_tuning.job",
  "id": "ftjob-abc123",
  "model": "gpt-4o-mini-2024-07-18",
  "created_at": 1721764800,
  "fine_tuned_model": null,
  "organization_id": "org-123",
  "result_files": [],
  "status": "queued",
  "validation_file": "file-abc123",
  "training_file": "file-abc123"
}
```
