# Cancel eval run

Source: https://platform.openai.com/docs/api-reference/evals/cancelRun

`POST /v1/evals/{eval_id}/runs/{run_id}`

Cancel an ongoing evaluation run.

## Parameters
- `eval_id` (path, string, required): The ID of the evaluation whose run you want to cancel.
- `run_id` (path, string, required): The ID of the run to cancel.

## Responses
### 200
The canceled eval run object
#### application/json
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
        - `type` (string, required): The type of jsonl source. Always `file_content`. Enum: 'file_content'. Default: `file_content`.
        - `content` (array<object>, required): The content of the jsonl file.
          - Items:
            - ...
      - Variant (object):
        - `type` (string, required): The type of jsonl source. Always `file_id`. Enum: 'file_id'. Default: `file_id`.
        - `id` (string, required): The identifier of the file.
  - Variant (object):
    - `type` (string, required): The type of run data source. Always `completions`. Enum: 'completions'. Default: `completions`.
    - `input_messages` (object, optional): Used when sampling from a model. Dictates the structure of the messages passed into the model. Can either be a reference to a prebuilt trajectory (ie, `item.input_trajectory`), or a template with variable references to the `item` namespace.
      - Variant (object):
        - `type` (string, required): The type of input messages. Always `template`. Enum: 'template'.
        - `template` (array<object>, required): A list of chat messages forming the prompt or context. May include variable references to the `item` namespace, ie {{item.name}}.
      - Variant (object):
        - `type` (string, required): The type of input messages. Always `item_reference`. Enum: 'item_reference'.
        - `item_reference` (string, required): A reference to a variable in the `item` namespace. Ie, "item.input_trajectory"
    - `sampling_params` (object, optional)
      - `reasoning_effort` (string | null, optional)
      - `temperature` (number, optional): A higher temperature increases randomness in the outputs. Default: `1`.
      - `max_completion_tokens` (integer, optional): The maximum number of tokens in the generated output.
      - `top_p` (number, optional): An alternative to temperature for nucleus sampling; 1.0 includes all tokens. Default: `1`.
      - `seed` (integer, optional): A seed value to initialize the randomness, during sampling. Default: `42`.
      - `response_format` (object, optional): An object specifying the format that the model must output.
        
        Setting to `{ "type": "json_schema", "json_schema": {...} }` enables
        Structured Outputs which ensures the model will match your supplied JSON
        schema. Learn more in the [Structured Outputs
        guide](https://platform.openai.com/docs/guides/structured-outputs).
        
        Setting to `{ "type": "json_object" }` enables the older JSON mode, which
        ensures the message the model generates is valid JSON. Using `json_schema`
        is preferred for models that support it.
        - Variant (object):
          - ...
        - Variant (object):
          - ...
        - Variant (object):
          - ...
      - `tools` (array<object>, optional): A list of tools the model may call. Currently, only functions are supported as a tool. Use this to provide a list of functions the model may generate JSON inputs for. A max of 128 functions are supported.
        - Items:
          - ...
    - `model` (string, optional): The name of the model to use for generating completions (e.g. "o3-mini").
    - `source` (object, required): Determines what populates the `item` namespace in this run's data source.
      - Variant (object):
        - `type` (string, required): The type of jsonl source. Always `file_content`. Enum: 'file_content'. Default: `file_content`.
        - `content` (array<object>, required): The content of the jsonl file.
          - Items:
            - ...
      - Variant (object):
        - `type` (string, required): The type of jsonl source. Always `file_id`. Enum: 'file_id'. Default: `file_id`.
        - `id` (string, required): The identifier of the file.
      - Variant (object):
        - `type` (string, required): The type of source. Always `stored_completions`. Enum: 'stored_completions'. Default: `stored_completions`.
        - `metadata` (object | null, optional)
        - `model` (string | null, optional)
        - `created_after` (integer | null, optional)
        - `created_before` (integer | null, optional)
        - `limit` (integer | null, optional)
  - Variant (object):
    - `type` (string, required): The type of run data source. Always `responses`. Enum: 'responses'. Default: `responses`.
    - `input_messages` (object, optional): Used when sampling from a model. Dictates the structure of the messages passed into the model. Can either be a reference to a prebuilt trajectory (ie, `item.input_trajectory`), or a template with variable references to the `item` namespace.
      - Variant (object):
        - `type` (string, required): The type of input messages. Always `template`. Enum: 'template'.
        - `template` (array<object>, required): A list of chat messages forming the prompt or context. May include variable references to the `item` namespace, ie {{item.name}}.
      - Variant (object):
        - `type` (string, required): The type of input messages. Always `item_reference`. Enum: 'item_reference'.
        - `item_reference` (string, required): A reference to a variable in the `item` namespace. Ie, "item.name"
    - `sampling_params` (object, optional)
      - `reasoning_effort` (string | null, optional)
      - `temperature` (number, optional): A higher temperature increases randomness in the outputs. Default: `1`.
      - `max_completion_tokens` (integer, optional): The maximum number of tokens in the generated output.
      - `top_p` (number, optional): An alternative to temperature for nucleus sampling; 1.0 includes all tokens. Default: `1`.
      - `seed` (integer, optional): A seed value to initialize the randomness, during sampling. Default: `42`.
      - `tools` (array<object>, optional): An array of tools the model may call while generating a response. You
        can specify which tool to use by setting the `tool_choice` parameter.
        
        The two categories of tools you can provide the model are:
        
        - **Built-in tools**: Tools that are provided by OpenAI that extend the
          model's capabilities, like [web search](https://platform.openai.com/docs/guides/tools-web-search)
          or [file search](https://platform.openai.com/docs/guides/tools-file-search). Learn more about
          [built-in tools](https://platform.openai.com/docs/guides/tools).
        - **Function calls (custom tools)**: Functions that are defined by you,
          enabling the model to call your own code. Learn more about
          [function calling](https://platform.openai.com/docs/guides/function-calling).
      - `text` (object, optional): Configuration options for a text response from the model. Can be plain
        text or structured JSON data. Learn more:
        - [Text inputs and outputs](https://platform.openai.com/docs/guides/text)
        - [Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)
        - `format` (object, optional): An object specifying the format that the model must output.
          
          Configuring `{ "type": "json_schema" }` enables Structured Outputs, 
          which ensures the model will match your supplied JSON schema. Learn more in the 
          [Structured Outputs guide](https://platform.openai.com/docs/guides/structured-outputs).
          
          The default format is `{ "type": "text" }` with no additional options.
          
          **Not recommended for gpt-4o and newer models:**
          
          Setting to `{ "type": "json_object" }` enables the older JSON mode, which
          ensures the message the model generates is valid JSON. Using `json_schema`
          is preferred for models that support it.
          - Variant (object):
            - ...
          - Variant (object):
            - ...
          - Variant (object):
            - ...
    - `model` (string, optional): The name of the model to use for generating completions (e.g. "o3-mini").
    - `source` (object, required): Determines what populates the `item` namespace in this run's data source.
      - Variant (object):
        - `type` (string, required): The type of jsonl source. Always `file_content`. Enum: 'file_content'. Default: `file_content`.
        - `content` (array<object>, required): The content of the jsonl file.
          - Items:
            - ...
      - Variant (object):
        - `type` (string, required): The type of jsonl source. Always `file_id`. Enum: 'file_id'. Default: `file_id`.
        - `id` (string, required): The identifier of the file.
      - Variant (object):
        - `type` (string, required): The type of run data source. Always `responses`. Enum: 'responses'.
        - `metadata` (object | null, optional)
        - `model` (string | null, optional)
        - `instructions_search` (string | null, optional)
        - `created_after` (integer | null, optional)
        - `created_before` (integer | null, optional)
        - `reasoning_effort` (string | null | null, optional)
        - `temperature` (number | null, optional)
        - `top_p` (number | null, optional)
        - `users` (array<string> | null, optional)
        - `tools` (array<string> | null, optional)
- `metadata` (object | null, required)
- `error` (object, required): An object representing an error response from the Eval API.
  - `code` (string, required): The error code.
  - `message` (string, required): The error message.

## Returns
The updated [EvalRun](run-object.md) object reflecting that the run is canceled.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/evals/eval_67abd54d9b0081909a86353f6fb9317a/runs/evalrun_67abd54d60ec8190832b46859da808f7/cancel \
  -X POST \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

canceled_run = client.evals.runs.cancel(
  "eval_67abd54d9b0081909a86353f6fb9317a",
  "evalrun_67abd54d60ec8190832b46859da808f7"
)
print(canceled_run)
```
#### Response
```json
{
  "object": "eval.run",
  "id": "evalrun_67abd54d60ec8190832b46859da808f7",
  "eval_id": "eval_67abd54d9b0081909a86353f6fb9317a",
  "report_url": "https://platform.openai.com/evaluations/eval_67abd54d9b0081909a86353f6fb9317a?run_id=evalrun_67abd54d60ec8190832b46859da808f7",
  "status": "canceled",
  "model": "gpt-4o-mini",
  "name": "gpt-4o-mini",
  "created_at": 1743092069,
  "result_counts": {
    "total": 0,
    "errored": 0,
    "failed": 0,
    "passed": 0
  },
  "per_model_usage": null,
  "per_testing_criteria_results": null,
  "data_source": {
    "type": "completions",
    "source": {
      "type": "file_content",
      "content": [
        {
          "item": {
            "input": "Tech Company Launches Advanced Artificial Intelligence Platform",
            "ground_truth": "Technology"
          }
        },
        {
          "item": {
            "input": "Central Bank Increases Interest Rates Amid Inflation Concerns",
            "ground_truth": "Markets"
          }
        },
        {
          "item": {
            "input": "International Summit Addresses Climate Change Strategies",
            "ground_truth": "World"
          }
        },
        {
          "item": {
            "input": "Major Retailer Reports Record-Breaking Holiday Sales",
            "ground_truth": "Business"
          }
        },
        {
          "item": {
            "input": "National Team Qualifies for World Championship Finals",
            "ground_truth": "Sports"
          }
        },
        {
          "item": {
            "input": "Stock Markets Rally After Positive Economic Data Released",
            "ground_truth": "Markets"
          }
        },
        {
          "item": {
            "input": "Global Manufacturer Announces Merger with Competitor",
            "ground_truth": "Business"
          }
        },
        {
          "item": {
            "input": "Breakthrough in Renewable Energy Technology Unveiled",
            "ground_truth": "Technology"
          }
        },
        {
          "item": {
            "input": "World Leaders Sign Historic Climate Agreement",
            "ground_truth": "World"
          }
        },
        {
          "item": {
            "input": "Professional Athlete Sets New Record in Championship Event",
            "ground_truth": "Sports"
          }
        },
        {
          "item": {
            "input": "Financial Institutions Adapt to New Regulatory Requirements",
            "ground_truth": "Business"
          }
        },
        {
          "item": {
            "input": "Tech Conference Showcases Advances in Artificial Intelligence",
            "ground_truth": "Technology"
          }
        },
        {
          "item": {
            "input": "Global Markets Respond to Oil Price Fluctuations",
            "ground_truth": "Markets"
          }
        },
        {
          "item": {
            "input": "International Cooperation Strengthened Through New Treaty",
            "ground_truth": "World"
          }
        },
        {
          "item": {
            "input": "Sports League Announces Revised Schedule for Upcoming Season",
            "ground_truth": "Sports"
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
            "text": "Categorize a given news headline into one of the following topics: Technology, Markets, World, Business, or Sports.\n\n# Steps\n\n1. Analyze the content of the news headline to understand its primary focus.\n2. Extract the subject matter, identifying any key indicators or keywords.\n3. Use the identified indicators to determine the most suitable category out of the five options: Technology, Markets, World, Business, or Sports.\n4. Ensure only one category is selected per headline.\n\n# Output Format\n\nRespond with the chosen category as a single word. For instance: \"Technology\", \"Markets\", \"World\", \"Business\", or \"Sports\".\n\n# Examples\n\n**Input**: \"Apple Unveils New iPhone Model, Featuring Advanced AI Features\"  \n**Output**: \"Technology\"\n\n**Input**: \"Global Stocks Mixed as Investors Await Central Bank Decisions\"  \n**Output**: \"Markets\"\n\n**Input**: \"War in Ukraine: Latest Updates on Negotiation Status\"  \n**Output**: \"World\"\n\n**Input**: \"Microsoft in Talks to Acquire Gaming Company for $2 Billion\"  \n**Output**: \"Business\"\n\n**Input**: \"Manchester United Secures Win in Premier League Football Match\"  \n**Output**: \"Sports\" \n\n# Notes\n\n- If the headline appears to fit into more than one category, choose the most dominant theme.\n- Keywords or phrases such as \"stocks\", \"company acquisition\", \"match\", or technological brands can be good indicators for classification.\n"
          }
        },
        {
          "type": "message",
          "role": "user",
          "content": {
            "type": "input_text",
            "text": "{{item.input}}"
          }
        }
      ]
    },
    "model": "gpt-4o-mini",
    "sampling_params": {
      "seed": 42,
      "temperature": 1.0,
      "top_p": 1.0,
      "max_completions_tokens": 2048
    }
  },
  "error": null,
  "metadata": {}
}
```
