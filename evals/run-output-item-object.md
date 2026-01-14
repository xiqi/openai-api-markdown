# The eval run output item object

Source: https://platform.openai.com/docs/api-reference/evals/run-output-item-object

A schema representing an evaluation run output item.

## Properties
- `object` (string, required): The type of the object. Always "eval.run.output_item". Enum: 'eval.run.output_item'. Default: `eval.run.output_item`.
- `id` (string, required): Unique identifier for the evaluation run output item.
- `run_id` (string, required): The identifier of the evaluation run associated with this output item.
- `eval_id` (string, required): The identifier of the evaluation group.
- `created_at` (integer, required): Unix timestamp (in seconds) when the evaluation run was created.
- `status` (string, required): The status of the evaluation run.
- `datasource_item_id` (integer, required): The identifier for the data source item.
- `datasource_item` (object, required): Details of the input data source item.
- `results` (array<object>, required): A list of grader results for this output item.
  - Items:
    - `name` (string, required): The name of the grader.
    - `type` (string, optional): The grader type (for example, "string-check-grader").
    - `score` (number, required): The numeric score produced by the grader.
    - `passed` (boolean, required): Whether the grader considered the output a pass.
    - `sample` (object | null, optional): Optional sample or intermediate data produced by the grader.
- `sample` (object, required): A sample containing the input and output of the evaluation run.
  - `input` (array<object>, required): An array of input messages.
    - Items:
      - `role` (string, required): The role of the message sender (e.g., system, user, developer).
      - `content` (string, required): The content of the message.
  - `output` (array<object>, required): An array of output messages.
    - Items:
      - `role` (string, optional): The role of the message (e.g. "system", "assistant", "user").
      - `content` (string, optional): The content of the message.
  - `finish_reason` (string, required): The reason why the sample generation was finished.
  - `model` (string, required): The model used for generating the sample.
  - `usage` (object, required): Token usage details for the sample.
    - `total_tokens` (integer, required): The total number of tokens used.
    - `completion_tokens` (integer, required): The number of completion tokens generated.
    - `prompt_tokens` (integer, required): The number of prompt tokens used.
    - `cached_tokens` (integer, required): The number of tokens retrieved from cache.
  - `error` (object, required): An object representing an error response from the Eval API.
    - `code` (string, required): The error code.
    - `message` (string, required): The error message.
  - `temperature` (number, required): The sampling temperature used.
  - `max_completion_tokens` (integer, required): The maximum number of tokens allowed for completion.
  - `top_p` (number, required): The top_p value used for sampling.
  - `seed` (integer, required): The seed used for generating the sample.
