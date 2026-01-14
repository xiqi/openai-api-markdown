# error

Source: https://platform.openai.com/docs/api-reference/realtime-beta-server-events/error

Returned when an error occurs, which could be a client problem or a server
problem. Most errors are recoverable and the session will stay open, we
recommend to implementors to monitor and log error messages by default.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `error`. Enum: 'error'.
- `error` (object, required): Details of the error.
  - `type` (string, required): The type of error (e.g., "invalid_request_error", "server_error").
  - `code` (string | null, optional)
  - `message` (string, required): A human-readable error message.
  - `param` (string | null, optional)
  - `event_id` (string | null, optional)
