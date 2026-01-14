# The eval object

Source: https://platform.openai.com/docs/api-reference/evals/object

An Eval object with a data source config and testing criteria.
An Eval represents a task to be done for your LLM integration.
Like:
 - Improve the quality of my chatbot
 - See how well my chatbot handles customer support
 - Check if o4-mini is better at my usecase than gpt-4o

## Properties
- `object` (string, required): The object type. Enum: 'eval'. Default: `eval`.
- `id` (string, required): Unique identifier for the evaluation.
- `name` (string, required): The name of the evaluation.
- `data_source_config` (object, required): Configuration of data sources used in runs of the evaluation.
  - Variant (object):
    - `type` (string, required): The type of data source. Always `custom`. Enum: 'custom'. Default: `custom`.
    - `schema` (object, required): The json schema for the run data source items.
      Learn how to build JSON schemas [here](https://json-schema.org/).
  - Variant (object):
    - `type` (string, required): The type of data source. Always `logs`. Enum: 'logs'. Default: `logs`.
    - `metadata` (object | null, optional)
    - `schema` (object, required): The json schema for the run data source items.
      Learn how to build JSON schemas [here](https://json-schema.org/).
  - Variant (object):
    - `type` (string, required): The type of data source. Always `stored_completions`. Enum: 'stored_completions'. Default: `stored_completions`.
    - `metadata` (object | null, optional)
    - `schema` (object, required): The json schema for the run data source items.
      Learn how to build JSON schemas [here](https://json-schema.org/).
- `testing_criteria` (array<object>, required): A list of testing criteria. Default: `eval`.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the eval was created.
- `metadata` (object | null, required)
