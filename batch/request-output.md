# The request output object

Source: https://platform.openai.com/docs/api-reference/batch/request-output

The per-line object of the batch output and error files

## Properties
- `id` (string, optional)
- `custom_id` (string, optional): A developer-provided per-request id that will be used to match outputs to inputs.
- `response` (object | null, optional)
  - Variant (object):
    - `status_code` (integer, optional): The HTTP status code of the response
    - `request_id` (string, optional): An unique identifier for the OpenAI API request. Please include this request ID when contacting support.
    - `body` (object, optional): The JSON body of the response
- `error` (object | null, optional)
  - Variant (object):
    - `code` (string, optional): A machine-readable error code.
      
      Possible values:
      - `batch_expired`: The request could not be executed before the
        completion window ended.
      - `batch_cancelled`: The batch was cancelled before this request
        executed.
      - `request_timeout`: The underlying call to the model timed out.
    - `message` (string, optional): A human-readable error message.
