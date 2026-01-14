# The input item list

Source: https://platform.openai.com/docs/api-reference/responses/list

A list of Response items.

## Properties
- `object` (string, required): The type of object returned, must be `list`. Enum: 'list'.
- `data` (array<object>, required): A list of items used to generate this response.
- `has_more` (boolean, required): Whether there are more items available.
- `first_id` (string, required): The ID of the first item in the list.
- `last_id` (string, required): The ID of the last item in the list.
