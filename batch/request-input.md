# The request input object

Source: https://platform.openai.com/docs/api-reference/batch/request-input

The per-line object of the batch input file

## Properties
- `custom_id` (string, optional): A developer-provided per-request id that will be used to match outputs to inputs. Must be unique for each request in a batch.
- `method` (string, optional): The HTTP method to be used for the request. Currently only `POST` is supported. Enum: 'POST'.
- `url` (string, optional): The OpenAI API relative URL to be used for the request. Currently `/v1/responses`, `/v1/chat/completions`, `/v1/embeddings`, `/v1/completions`, and `/v1/moderations` are supported.
