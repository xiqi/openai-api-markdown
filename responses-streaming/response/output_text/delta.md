# response.output_text.delta

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/output_text/delta

Emitted when there is an additional text delta.

## Properties
- `type` (string, required): The type of the event. Always `response.output_text.delta`. Enum: 'response.output_text.delta'.
- `item_id` (string, required): The ID of the output item that the text delta was added to.
- `output_index` (integer, required): The index of the output item that the text delta was added to.
- `content_index` (integer, required): The index of the content part that the text delta was added to.
- `delta` (string, required): The text delta that was added.
- `sequence_number` (integer, required): The sequence number for this event.
- `logprobs` (array<object>, required): The log probabilities of the tokens in the delta.
  - Items:
    - `token` (string, required): A possible text token.
    - `logprob` (number, required): The log probability of this token.
    - `top_logprobs` (array<object>, optional): The log probability of the top 20 most likely tokens.
      - Items:
        - `token` (string, optional): A possible text token.
        - `logprob` (number, optional): The log probability of this token.
