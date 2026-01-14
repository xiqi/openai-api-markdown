# Label Model Grader

Source: https://platform.openai.com/docs/api-reference/graders/label-model

A LabelModelGrader object which uses a model to assign labels to each item
in the evaluation.

## Properties
- `type` (string, required): The object type, which is always `label_model`. Enum: 'label_model'.
- `name` (string, required): The name of the grader.
- `model` (string, required): The model to use for the evaluation. Must support structured outputs.
- `input` (array<object>, required)
  - Items:
    - `role` (string, required): The role of the message input. One of `user`, `assistant`, `system`, or
      `developer`. Enum: 'user', 'assistant', 'system', 'developer'.
    - `content` (string | object | array<string | object>, required): Inputs to the model - can contain template strings. Supports text, output text, input images, and input audio, either as a single item or an array of items.
    - `type` (string, optional): The type of the message input. Always `message`. Enum: 'message'.
- `labels` (array<string>, required): The labels to assign to each item in the evaluation.
- `passing_labels` (array<string>, required): The labels that indicate a passing result. Must be a subset of labels.
