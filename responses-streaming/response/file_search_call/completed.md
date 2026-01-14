# response.file_search_call.completed

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/file_search_call/completed

Emitted when a file search call is completed (results found).

## Properties
- `type` (string, required): The type of the event. Always `response.file_search_call.completed`. Enum: 'response.file_search_call.completed'.
- `output_index` (integer, required): The index of the output item that the file search call is initiated.
- `item_id` (string, required): The ID of the output item that the file search call is initiated.
- `sequence_number` (integer, required): The sequence number of this event.
