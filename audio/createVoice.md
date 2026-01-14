# Create voice

Source: https://platform.openai.com/docs/api-reference/audio/createVoice

`POST /v1/audio/voices`

Creates a custom voice.

## Request body
### multipart/form-data
- `name` (string, required): The name of the new voice.
- `audio_sample` (string, required): The sample audio recording file. Maximum size is 10 MiB.
  
  Supported MIME types:
  `audio/mpeg`, `audio/wav`, `audio/x-wav`, `audio/ogg`, `audio/aac`, `audio/flac`, `audio/webm`, `audio/mp4`.
- `consent` (string, required): The consent recording ID (for example, `cons_1234`).

## Responses
### 200
OK
#### application/json
- `object` (string, required): The object type, which is always `audio.voice`. Enum: 'audio.voice'.
- `id` (string, required): The voice identifier, which can be referenced in API endpoints.
- `name` (string, required): The name of the voice.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the voice was created.

## Returns
The created voice.

## Examples
### Default
#### Request (curl)
```bash
curl https://api.openai.com/v1/audio/voices \
  -X POST \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F "name=My new voice" \
  -F "consent=cons_1234" \
  -F "audio_sample=@$HOME/audio_sample.wav;type=audio/x-wav"
```
