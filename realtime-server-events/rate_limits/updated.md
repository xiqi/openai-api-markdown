# rate_limits.updated

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/rate_limits/updated

Emitted at the beginning of a Response to indicate the updated rate limits. 
When a Response is created some tokens will be "reserved" for the output 
tokens, the rate limits shown here reflect that reservation, which is then 
adjusted accordingly once the Response is completed.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `rate_limits.updated`. Enum: 'rate_limits.updated'.
- `rate_limits` (array<object>, required): List of rate limit information.
  - Items:
    - `name` (string, optional): The name of the rate limit (`requests`, `tokens`). Enum: 'requests', 'tokens'.
    - `limit` (integer, optional): The maximum allowed value for the rate limit.
    - `remaining` (integer, optional): The remaining value before the limit is reached.
    - `reset_seconds` (number, optional): Seconds until the rate limit resets.
