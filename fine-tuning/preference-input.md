# Training format for chat models using the preference method

Source: https://platform.openai.com/docs/api-reference/fine-tuning/preference-input

The per-line training example of a fine-tuning input file for chat models using the dpo method.
Input messages may contain text or image content only. Audio and file input messages
are not currently supported for fine-tuning.

## Properties
- `input` (object, optional)
  - `messages` (array<object>, optional)
  - `tools` (array<object>, optional): A list of tools the model may generate JSON inputs for.
    - Items:
      - `type` (string, required): The type of the tool. Currently, only `function` is supported. Enum: 'function'.
      - `function` (object, required)
        - `description` (string, optional): A description of what the function does, used by the model to choose when and how to call the function.
        - `name` (string, required): The name of the function to be called. Must be a-z, A-Z, 0-9, or contain underscores and dashes, with a maximum length of 64.
        - `parameters` (object, optional): The parameters the functions accepts, described as a JSON Schema object. See the [guide](https://platform.openai.com/docs/guides/function-calling) for examples, and the [JSON Schema reference](https://json-schema.org/understanding-json-schema/) for documentation about the format. 
          
          Omitting `parameters` defines a function with an empty parameter list.
        - `strict` (boolean | null, optional)
  - `parallel_tool_calls` (boolean, optional): Whether to enable [parallel function calling](https://platform.openai.com/docs/guides/function-calling#configuring-parallel-function-calling) during tool use. Default: `True`.
- `preferred_output` (array<object>, optional): The preferred completion message for the output.
- `non_preferred_output` (array<object>, optional): The non-preferred completion message for the output.
