# Hang up call

Source: https://platform.openai.com/docs/api-reference/realtime-calls/hangup-call

`POST /v1/realtime/calls/{call_id}/hangup`

End an active Realtime API call, whether it was initiated over SIP or
WebRTC.

## Parameters
- `call_id` (path, string, required): The identifier for the call. For SIP calls, use the value provided in the
  [`realtime.call.incoming`](../webhook-events/realtime/call/incoming.md)
  webhook. For WebRTC sessions, reuse the call ID returned in the `Location`
  header when creating the call with
  [`POST /v1/realtime/calls`](../realtime/create-call.md).

## Responses
### 200
Call hangup initiated successfully.

## Returns
Returns `200 OK` when OpenAI begins terminating the realtime call.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/realtime/calls/$CALL_ID/hangup \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
