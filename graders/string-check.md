# String Check Grader

Source: https://platform.openai.com/docs/api-reference/graders/string-check

A StringCheckGrader object that performs a string comparison between input and reference using a specified operation.

## Properties
- `type` (string, required): The object type, which is always `string_check`. Enum: 'string_check'.
- `name` (string, required): The name of the grader.
- `input` (string, required): The input text. This may include template strings.
- `reference` (string, required): The reference text. This may include template strings.
- `operation` (string, required): The string check operation to perform. One of `eq`, `ne`, `like`, or `ilike`. Enum: 'eq', 'ne', 'like', 'ilike'.
