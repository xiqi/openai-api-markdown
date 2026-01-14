# error

Source: https://platform.openai.com/docs/api-reference/responses-streaming/error

Emitted when an error occurs.

## Properties
- `type` (string, required): The type of the event. Always `error`. Enum: 'error'.
- `code` (string | null, required)
- `message` (string, required): The error message.
- `param` (string | null, required)
- `sequence_number` (integer, required): The sequence number of this event.
