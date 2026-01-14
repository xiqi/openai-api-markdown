# Delete voice consent

Source: https://platform.openai.com/docs/api-reference/audio/deleteVoiceConsent

`DELETE /v1/audio/voice_consents/{consent_id}`

Deletes a voice consent recording.

## Parameters
- `consent_id` (path, string, required): The ID of the consent recording to delete.

## Responses
### 200
OK
#### application/json
- `id` (string, required): The consent recording identifier.
- `object` (string, required) Enum: 'audio.voice_consent'.
- `deleted` (boolean, required)

## Returns
A deletion confirmation.

## Examples
### Default
#### Request (curl)
```bash
curl https://api.openai.com/v1/audio/voice_consents/cons_1234 \
  -X DELETE \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
