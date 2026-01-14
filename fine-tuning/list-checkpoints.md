# List fine-tuning checkpoints

Source: https://platform.openai.com/docs/api-reference/fine-tuning/list-checkpoints

`GET /v1/fine_tuning/jobs/{fine_tuning_job_id}/checkpoints`

List checkpoints for a fine-tuning job.

## Parameters
- `fine_tuning_job_id` (path, string, required): The ID of the fine-tuning job to get checkpoints for.
- `after` (query, string, optional): Identifier for the last checkpoint ID from the previous pagination request.
- `limit` (query, integer, optional): Number of checkpoints to retrieve. Default: `10`.

## Responses
### 200
OK
#### application/json
- `data` (array<object>, required)
  - Items:
    - `id` (string, required): The checkpoint identifier, which can be referenced in the API endpoints.
    - `created_at` (integer, required): The Unix timestamp (in seconds) for when the checkpoint was created.
    - `fine_tuned_model_checkpoint` (string, required): The name of the fine-tuned checkpoint model that is created.
    - `step_number` (integer, required): The step number that the checkpoint was created at.
    - `metrics` (object, required): Metrics at the step number during the fine-tuning job.
      - `step` (number, optional)
      - `train_loss` (number, optional)
      - `train_mean_token_accuracy` (number, optional)
      - `valid_loss` (number, optional)
      - `valid_mean_token_accuracy` (number, optional)
      - `full_valid_loss` (number, optional)
      - `full_valid_mean_token_accuracy` (number, optional)
    - `fine_tuning_job_id` (string, required): The name of the fine-tuning job that this checkpoint was created from.
    - `object` (string, required): The object type, which is always "fine_tuning.job.checkpoint". Enum: 'fine_tuning.job.checkpoint'.
- `object` (string, required) Enum: 'list'.
- `first_id` (string | null, optional)
- `last_id` (string | null, optional)
- `has_more` (boolean, required)

## Returns
A list of fine-tuning [checkpoint objects](checkpoint-object.md) for a fine-tuning job.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/fine_tuning/jobs/ftjob-abc123/checkpoints \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "object": "fine_tuning.job.checkpoint",
      "id": "ftckpt_zc4Q7MP6XxulcVzj4MZdwsAB",
      "created_at": 1721764867,
      "fine_tuned_model_checkpoint": "ft:gpt-4o-mini-2024-07-18:my-org:custom-suffix:96olL566:ckpt-step-2000",
      "metrics": {
        "full_valid_loss": 0.134,
        "full_valid_mean_token_accuracy": 0.874
      },
      "fine_tuning_job_id": "ftjob-abc123",
      "step_number": 2000
    },
    {
      "object": "fine_tuning.job.checkpoint",
      "id": "ftckpt_enQCFmOTGj3syEpYVhBRLTSy",
      "created_at": 1721764800,
      "fine_tuned_model_checkpoint": "ft:gpt-4o-mini-2024-07-18:my-org:custom-suffix:7q8mpxmy:ckpt-step-1000",
      "metrics": {
        "full_valid_loss": 0.167,
        "full_valid_mean_token_accuracy": 0.781
      },
      "fine_tuning_job_id": "ftjob-abc123",
      "step_number": 1000
    }
  ],
  "first_id": "ftckpt_zc4Q7MP6XxulcVzj4MZdwsAB",
  "last_id": "ftckpt_enQCFmOTGj3syEpYVhBRLTSy",
  "has_more": true
}
```
