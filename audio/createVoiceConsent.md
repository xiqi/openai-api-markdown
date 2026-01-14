# Create voice consent

Source: https://platform.openai.com/docs/api-reference/audio/createVoiceConsent

`POST /v1/audio/voice_consents`

Upload a voice consent recording.

## Request body
### multipart/form-data
- `name` (string, required): The label to use for this consent recording.
- `recording` (string, required): The consent audio recording file. Maximum size is 10 MiB.
  
  Supported MIME types:
  `audio/mpeg`, `audio/wav`, `audio/x-wav`, `audio/ogg`, `audio/aac`, `audio/flac`, `audio/webm`, `audio/mp4`.
- `language` (string, required): The BCP 47 language tag for the consent phrase (for example, `en-US`).

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
The created voice consent recording metadata.

## Examples
### Default
#### Request (curl)
```bash
curl https://api.openai.com/v1/audio/voice_consents \
  -X POST \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F "name=John Doe" \
  -F "language=en-US" \
  -F "recording=@$HOME/consent_recording.wav;type=audio/x-wav"
```
