# The conversation object

Source: https://platform.openai.com/docs/api-reference/conversations/object

## Properties
- `id` (string, required): The unique ID of the conversation.
- `object` (string, required): The object type, which is always `conversation`. Enum: 'conversation'. Default: `conversation`.
- `metadata` (object, required): Set of 16 key-value pairs that can be attached to an object. This can be         useful for storing additional information about the object in a structured         format, and querying for objects via API or the dashboard.
          Keys are strings with a maximum length of 64 characters. Values are strings         with a maximum length of 512 characters.
- `created_at` (integer, required): The time at which the conversation was created, measured in seconds since the Unix epoch.
