# The fine-tuning job checkpoint object

Source: https://platform.openai.com/docs/api-reference/fine-tuning/checkpoint-object

The `fine_tuning.job.checkpoint` object represents a model checkpoint for a fine-tuning job that is ready to use.

## Properties
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
