# Run grader

Source: https://platform.openai.com/docs/api-reference/graders/run

`POST /v1/fine_tuning/alpha/graders/run`

Run a grader.

## Request body
### application/json
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
          - ...
        - `input` (array<object>, required): The input messages evaluated by the grader. Supports text, output text, input image, and input audio content blocks, and may include template strings.
          - Items:
            - ...
        - `range` (array<number>, optional): The range of the score. Defaults to `[0, 1]`.
      - Variant (object):
        - `type` (string, required): The object type, which is always `label_model`. Enum: 'label_model'.
        - `name` (string, required): The name of the grader.
        - `model` (string, required): The model to use for the evaluation. Must support structured outputs.
        - `input` (array<object>, required)
          - Items:
            - ...
        - `labels` (array<string>, required): The labels to assign to each item in the evaluation.
        - `passing_labels` (array<string>, required): The labels that indicate a passing result. Must be a subset of labels.
    - `calculate_output` (string, required): A formula to calculate the output based on grader results.
- `item` (object, optional): The dataset item provided to the grader. This will be used to populate 
  the `item` namespace. See [the guide](https://platform.openai.com/docs/guides/graders) for more details.
- `model_sample` (string, required): The model sample to be evaluated. This value will be used to populate 
  the `sample` namespace. See [the guide](https://platform.openai.com/docs/guides/graders) for more details.
  The `output_json` variable will be populated if the model sample is a 
  valid JSON string.

## Responses
### 200
OK
#### application/json
- `reward` (number, required)
- `metadata` (object, required)
  - `name` (string, required)
  - `type` (string, required)
  - `errors` (object, required)
    - `formula_parse_error` (boolean, required)
    - `sample_parse_error` (boolean, required)
    - `truncated_observation_error` (boolean, required)
    - `unresponsive_reward_error` (boolean, required)
    - `invalid_variable_error` (boolean, required)
    - `other_error` (boolean, required)
    - `python_grader_server_error` (boolean, required)
    - `python_grader_server_error_type` (string | null, required)
    - `python_grader_runtime_error` (boolean, required)
    - `python_grader_runtime_error_details` (string | null, required)
    - `model_grader_server_error` (boolean, required)
    - `model_grader_refusal_error` (boolean, required)
    - `model_grader_parse_error` (boolean, required)
    - `model_grader_server_error_details` (string | null, required)
  - `execution_time` (number, required)
  - `scores` (object, required)
  - `token_usage` (integer | null, required)
  - `sampled_model_name` (string | null, required)
- `sub_rewards` (object, required)
- `model_grader_token_usage_per_model` (object, required)

## Returns
The results from the grader run.

## Examples
### Score text alignment
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/fine_tuning/alpha/graders/run \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "grader": {
      "type": "score_model",
      "name": "Example score model grader",
      "input": [
        {
          "role": "user",
          "content": [
            {
              "type": "input_text",
              "text": "Score how close the reference answer is to the model answer on a 0-1 scale. Return only the score.\n\nReference answer: {{item.reference_answer}}\n\nModel answer: {{sample.output_text}}"
            }
          ]
        }
      ],
      "model": "gpt-5-mini",
      "sampling_params": {
        "temperature": 1,
        "top_p": 1,
        "seed": 42
      }
    },
    "item": {
      "reference_answer": "fuzzy wuzzy was a bear"
    },
    "model_sample": "fuzzy wuzzy was a bear"
  }'
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
result = client.fine_tuning.alpha.graders.run(
  grader={
    "type": "score_model",
    "name": "Example score model grader",
    "input": [
      {
        "role": "user",
        "content": [
          {
            "type": "input_text",
            "text": "Score how close the reference answer is to the model answer on a 0-1 scale. Return only the score.\n\nReference answer: {{item.reference_answer}}\n\nModel answer: {{sample.output_text}}",
          }
        ],
      }
    ],
    "model": "gpt-5-mini",
    "sampling_params": {"temperature": 1, "top_p": 1, "seed": 42},
  },
  item={"reference_answer": "fuzzy wuzzy was a bear"},
  model_sample="fuzzy wuzzy was a bear",
)
print(result)
```
#### Response
```json
{
  "reward": 1.0,
  "metadata": {
    "name": "Example score model grader",
    "type": "score_model",
    "errors": {
      "formula_parse_error": false,
      "sample_parse_error": false,
      "truncated_observation_error": false,
      "unresponsive_reward_error": false,
      "invalid_variable_error": false,
      "other_error": false,
      "python_grader_server_error": false,
      "python_grader_server_error_type": null,
      "python_grader_runtime_error": false,
      "python_grader_runtime_error_details": null,
      "model_grader_server_error": false,
      "model_grader_refusal_error": false,
      "model_grader_parse_error": false,
      "model_grader_server_error_details": null
    },
    "execution_time": 4.365238428115845,
    "scores": {},
    "token_usage": {
      "prompt_tokens": 190,
      "total_tokens": 324,
      "completion_tokens": 134,
      "cached_tokens": 0
    },
    "sampled_model_name": "gpt-4o-2024-08-06"
  },
  "sub_rewards": {},
  "model_grader_token_usage_per_model": {
    "gpt-4o-2024-08-06": {
      "prompt_tokens": 190,
      "total_tokens": 324,
      "completion_tokens": 134,
      "cached_tokens": 0
    }
  }
}
```
### Score an image caption
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/fine_tuning/alpha/graders/run \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "grader": {
      "type": "score_model",
      "name": "Image caption grader",
      "input": [
        {
          "role": "user",
          "content": [
            {
              "type": "input_text",
              "text": "Score how well the provided caption matches the image on a 0-1 scale. Only return the score.\n\nCaption: {{sample.output_text}}"
            },
            {
              "type": "input_image",
              "image_url": "https://example.com/dog-catching-ball.png",
              "file_id": null,
              "detail": "high"
            }
          ]
        }
      ],
      "model": "gpt-5-mini",
      "sampling_params": {
        "temperature": 0.2
      }
    },
    "item": {
      "expected_caption": "A golden retriever jumps to catch a tennis ball"
    },
    "model_sample": "A dog leaps to grab a tennis ball mid-air"
  }'
```
### Score an audio response
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/fine_tuning/alpha/graders/run \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "grader": {
      "type": "score_model",
      "name": "Audio clarity grader",
      "input": [
        {
          "role": "user",
          "content": [
            {
              "type": "input_text",
              "text": "Listen to the clip and return a confidence score from 0 to 1 that the speaker said: {{item.target_phrase}}"
            },
            {
              "type": "input_audio",
              "input_audio": {
                "data": "{{item.audio_clip_b64}}",
                "format": "mp3"
              }
            }
          ]
        }
      ],
      "model": "gpt-audio",
      "sampling_params": {
        "temperature": 0.2,
        "top_p": 1,
        "seed": 123
      }
    },
    "item": {
      "target_phrase": "Please deliver the package on Tuesday",
      "audio_clip_b64": "<base64-encoded mp3>"
    },
    "model_sample": "Please deliver the package on Tuesday"
  }'
```
