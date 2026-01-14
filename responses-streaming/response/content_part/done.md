# response.content_part.done

Source: https://platform.openai.com/docs/api-reference/responses-streaming/response/content_part/done

Emitted when a content part is done.

## Properties
- `type` (string, required): The type of the event. Always `response.content_part.done`. Enum: 'response.content_part.done'.
- `item_id` (string, required): The ID of the output item that the content part was added to.
- `output_index` (integer, required): The index of the output item that the content part was added to.
- `content_index` (integer, required): The index of the content part that is done.
- `sequence_number` (integer, required): The sequence number of this event.
- `part` (object, required): The content part that is done.
  - Variant (object):
    - `type` (string, required): The type of the output text. Always `output_text`. Enum: 'output_text'. Default: `output_text`.
    - `text` (string, required): The text output from the model.
    - `annotations` (array<object>, required): The annotations of the text output.
    - `logprobs` (array<object>, required)
      - Items:
        - `token` (string, required)
        - `logprob` (number, required)
        - `bytes` (array<integer>, required)
        - `top_logprobs` (array<object>, required)
          - Items:
            - ...
  - Variant (object):
    - `type` (string, required): The type of the refusal. Always `refusal`. Enum: 'refusal'. Default: `refusal`.
    - `refusal` (string, required): The refusal explanation from the model.
  - Variant (object):
    - `type` (string, required): The type of the reasoning text. Always `reasoning_text`. Enum: 'reasoning_text'. Default: `reasoning_text`.
    - `text` (string, required): The reasoning text from the model.
