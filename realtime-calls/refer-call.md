# Refer call

Source: https://platform.openai.com/docs/api-reference/realtime-calls/refer-call

`POST /v1/realtime/calls/{call_id}/refer`

Transfer an active SIP call to a new destination using the SIP REFER verb.

## Parameters
- `call_id` (path, string, required): The identifier for the call provided in the
  [`realtime.call.incoming`](../webhook-events/realtime/call/incoming.md)
  webhook.

## Request body
### application/json
- `target_uri` (string, required): URI that should appear in the SIP Refer-To header. Supports values like
  `tel:+14155550123` or `sip:agent@example.com`.

## Responses
### 200
Call referred successfully.

## Returns
Returns `200 OK` once the REFER is handed off to your SIP provider.

## Examples
### Example
#### Request (curl)
```bash
curl -X POST https://api.openai.com/v1/realtime/calls/$CALL_ID/refer \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"target_uri": "tel:+14155550123"}'
```
