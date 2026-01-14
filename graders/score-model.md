# Score Model Grader

Source: https://platform.openai.com/docs/api-reference/graders/score-model

A ScoreModelGrader object that uses a model to assign a score to the input.

## Properties
- `type` (string, required): The object type, which is always `score_model`. Enum: 'score_model'.
- `name` (string, required): The name of the grader.
- `model` (string, required): The model to use for the evaluation.
- `sampling_params` (object, optional): The sampling parameters for the model.
  - `seed` (integer | null, optional)
  - `top_p` (number | null, optional)
  - `temperature` (number | null, optional)
  - `max_completions_tokens` (integer | null, optional)
  - `reasoning_effort` (string | null, optional)
- `input` (array<object>, required): The input messages evaluated by the grader. Supports text, output text, input image, and input audio content blocks, and may include template strings.
  - Items:
    - `role` (string, required): The role of the message input. One of `user`, `assistant`, `system`, or
      `developer`. Enum: 'user', 'assistant', 'system', 'developer'.
    - `content` (string | object | array<string | object>, required): Inputs to the model - can contain template strings. Supports text, output text, input images, and input audio, either as a single item or an array of items.
    - `type` (string, optional): The type of the message input. Always `message`. Enum: 'message'.
- `range` (array<number>, optional): The range of the score. Defaults to `[0, 1]`.
