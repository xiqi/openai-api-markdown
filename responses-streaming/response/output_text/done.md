# response.output_text.done

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/output_text/done

Emitted when text content is finalized.

## Properties
- `type` (string, required): The type of the event. Always `response.output_text.done`. Enum: 'response.output_text.done'.
- `item_id` (string, required): The ID of the output item that the text content is finalized.
- `output_index` (integer, required): The index of the output item that the text content is finalized.
- `content_index` (integer, required): The index of the content part that the text content is finalized.
- `text` (string, required): The text content that is finalized.
- `sequence_number` (integer, required): The sequence number for this event.
- `logprobs` (array<object>, required): The log probabilities of the tokens in the delta.
  - Items:
    - `token` (string, required): A possible text token.
    - `logprob` (number, required): The log probability of this token.
    - `top_logprobs` (array<object>, optional): The log probability of the top 20 most likely tokens.
      - Items:
        - `token` (string, optional): A possible text token.
        - `logprob` (number, optional): The log probability of this token.
