# Get an output item of an eval run

Source: https://platform.openai.com/docs/api-reference/evals/getRunOutputItem

`GET /v1/evals/{eval_id}/runs/{run_id}/output_items/{output_item_id}`

Get an evaluation run output item by ID.

## Parameters
- `eval_id` (path, string, required): The ID of the evaluation to retrieve runs for.
- `run_id` (path, string, required): The ID of the run to retrieve.
- `output_item_id` (path, string, required): The ID of the output item to retrieve.

## Responses
### 200
The evaluation run output item
#### application/json
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

## Returns
The [EvalRunOutputItem](run-output-item-object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/evals/eval_67abd54d9b0081909a86353f6fb9317a/runs/evalrun_67abd54d60ec8190832b46859da808f7/output_items/outputitem_67abd55eb6548190bb580745d5644a33 \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

output_item = client.evals.runs.output_items.retrieve(
  "eval_67abd54d9b0081909a86353f6fb9317a",
  "evalrun_67abd54d60ec8190832b46859da808f7",
  "outputitem_67abd55eb6548190bb580745d5644a33"
)
print(output_item)
```
#### Response
```json
{
  "object": "eval.run.output_item",
  "id": "outputitem_67e5796c28e081909917bf79f6e6214d",
  "created_at": 1743092076,
  "run_id": "evalrun_67abd54d60ec8190832b46859da808f7",
  "eval_id": "eval_67abd54d9b0081909a86353f6fb9317a",
  "status": "pass",
  "datasource_item_id": 5,
  "datasource_item": {
    "input": "Stock Markets Rally After Positive Economic Data Released",
    "ground_truth": "Markets"
  },
  "results": [
    {
      "name": "String check-a2486074-d803-4445-b431-ad2262e85d47",
      "sample": null,
      "passed": true,
      "score": 1.0
    }
  ],
  "sample": {
    "input": [
      {
        "role": "developer",
        "content": "Categorize a given news headline into one of the following topics: Technology, Markets, World, Business, or Sports.\n\n# Steps\n\n1. Analyze the content of the news headline to understand its primary focus.\n2. Extract the subject matter, identifying any key indicators or keywords.\n3. Use the identified indicators to determine the most suitable category out of the five options: Technology, Markets, World, Business, or Sports.\n4. Ensure only one category is selected per headline.\n\n# Output Format\n\nRespond with the chosen category as a single word. For instance: \"Technology\", \"Markets\", \"World\", \"Business\", or \"Sports\".\n\n# Examples\n\n**Input**: \"Apple Unveils New iPhone Model, Featuring Advanced AI Features\"  \n**Output**: \"Technology\"\n\n**Input**: \"Global Stocks Mixed as Investors Await Central Bank Decisions\"  \n**Output**: \"Markets\"\n\n**Input**: \"War in Ukraine: Latest Updates on Negotiation Status\"  \n**Output**: \"World\"\n\n**Input**: \"Microsoft in Talks to Acquire Gaming Company for $2 Billion\"  \n**Output**: \"Business\"\n\n**Input**: \"Manchester United Secures Win in Premier League Football Match\"  \n**Output**: \"Sports\" \n\n# Notes\n\n- If the headline appears to fit into more than one category, choose the most dominant theme.\n- Keywords or phrases such as \"stocks\", \"company acquisition\", \"match\", or technological brands can be good indicators for classification.\n",
        "tool_call_id": null,
        "tool_calls": null,
        "function_call": null
      },
      {
        "role": "user",
        "content": "Stock Markets Rally After Positive Economic Data Released",
        "tool_call_id": null,
        "tool_calls": null,
        "function_call": null
      }
    ],
    "output": [
      {
        "role": "assistant",
        "content": "Markets",
        "tool_call_id": null,
        "tool_calls": null,
        "function_call": null
      }
    ],
    "finish_reason": "stop",
    "model": "gpt-4o-mini-2024-07-18",
    "usage": {
      "total_tokens": 325,
      "completion_tokens": 2,
      "prompt_tokens": 323,
      "cached_tokens": 0
    },
    "error": null,
    "temperature": 1.0,
    "max_completion_tokens": 2048,
    "top_p": 1.0,
    "seed": 42
  }
}
```
