# Update voice consent

Source: https://platform.openai.com/docs/api-reference/audio/updateVoiceConsent

`POST /v1/audio/voice_consents/{consent_id}`

Updates a voice consent recording (metadata only).

## Parameters
- `consent_id` (path, string, required): The ID of the consent recording to update.

## Request body
### application/json
- `name` (string, required): The updated label for this consent recording.

## Responses
### 200
OK
#### application/json
- `object` (string, required): The object type, which is always `audio.voice_consent`. Enum: 'audio.voice_consent'.
- `id` (string, required): The consent recording identifier.
- `name` (string, required): The label provided when the consent recording was uploaded.
- `language` (string, required): The BCP 47 language tag for the consent phrase (for example, `en-US`).
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the consent recording was created.

## Returns
The updated voice consent recording metadata.

## Examples
### Default
#### Request (curl)
```bash
curl https://api.openai.com/v1/audio/voice_consents/cons_1234 \
  -X POST \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe"
  }'
```
