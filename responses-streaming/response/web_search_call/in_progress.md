# response.web_search_call.in_progress

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/web_search_call/in_progress

Emitted when a web search call is initiated.

## Properties
- `type` (string, required): The type of the event. Always `response.web_search_call.in_progress`. Enum: 'response.web_search_call.in_progress'.
- `output_index` (integer, required): The index of the output item that the web search call is associated with.
- `item_id` (string, required): Unique ID for the output item associated with the web search call.
- `sequence_number` (integer, required): The sequence number of the web search call being processed.
