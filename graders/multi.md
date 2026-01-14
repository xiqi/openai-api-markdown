# Multi Grader

Source: https://platform.openai.com/docs/api-reference/graders/multi

A MultiGrader object combines the output of multiple graders to produce a single score.

## Properties
- `type` (string, required): The object type, which is always `multi`. Enum: 'multi'. Default: `multi`.
- `name` (string, required): The name of the grader.
- `graders` (object, required)
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
  - Variant (object):
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
- `calculate_output` (string, required): A formula to calculate the output based on grader results.
