# Reject call

Source: https://platform.openai.com/docs/api-reference/realtime-calls/reject-call

`POST /v1/realtime/calls/{call_id}/reject`

Decline an incoming SIP call by returning a SIP status code to the caller.

## Parameters
- `call_id` (path, string, required): The identifier for the call provided in the
  [`realtime.call.incoming`](../webhook-events/realtime/call/incoming.md)
  webhook.

## Request body
### application/json
- `status_code` (integer, optional): SIP response code to send back to the caller. Defaults to `603` (Decline)
  when omitted.

## Responses
### 200
Call rejected successfully.

## Returns
Returns `200 OK` after OpenAI sends the SIP status code to the caller.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/realtime/calls/$CALL_ID/reject \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"status_code": 486}'
```
