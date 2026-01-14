# response.file_search_call.searching

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/file_search_call/searching

Emitted when a file search is currently searching.

## Properties
- `type` (string, required): The type of the event. Always `response.file_search_call.searching`. Enum: 'response.file_search_call.searching'.
- `output_index` (integer, required): The index of the output item that the file search call is searching.
- `item_id` (string, required): The ID of the output item that the file search call is initiated.
- `sequence_number` (integer, required): The sequence number of this event.
