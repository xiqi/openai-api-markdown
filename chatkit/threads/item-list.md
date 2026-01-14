# Thread Items

Source: https://platform.openai.com/docs/api-reference/chatkit/threads/item-list

A paginated list of thread items rendered for the ChatKit API.

## Properties
- `object` (string, required): The type of object returned, must be `list`. Enum: 'list'. Default: `list`.
- `data` (array<object>, required): A list of items
- `first_id` (string | null, required)
- `last_id` (string | null, required)
- `has_more` (boolean, required): Whether there are more items available.
