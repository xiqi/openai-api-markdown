# The item list

Source: https://platform.openai.com/docs/api-reference/conversations/list-items-object

A list of Conversation items.

## Properties
- `object` (string, required): The type of object returned, must be `list`. Enum: 'list'.
- `data` (array<object>, required): A list of conversation items.
- `has_more` (boolean, required): Whether there are more items available.
- `first_id` (string, required): The ID of the first item in the list.
- `last_id` (string, required): The ID of the last item in the list.
