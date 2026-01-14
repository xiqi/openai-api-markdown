# realtime.call.incoming

Source: https://platform.openai.com/docs/api-reference/webhook-events/realtime/call/incoming

Sent when Realtime API Receives a incoming SIP call.

## Properties
- `created_at` (integer, required): The Unix timestamp (in seconds) of when the model response was completed.
- `id` (string, required): The unique ID of the event.
- `data` (object, required): Event data payload.
  - `call_id` (string, required): The unique ID of this call.
  - `sip_headers` (array<object>, required): Headers from the SIP Invite.
    - Items:
      - `name` (string, required): Name of the SIP Header.
      - `value` (string, required): Value of the SIP Header.
- `object` (string, optional): The object of the event. Always `event`. Enum: 'event'.
- `type` (string, required): The type of the event. Always `realtime.call.incoming`. Enum: 'realtime.call.incoming'.
