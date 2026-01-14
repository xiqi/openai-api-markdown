# The voice object

Source: https://platform.openai.com/docs/api-reference/audio/voice-object

A custom voice that can be used for audio output.

## Properties
- `object` (string, required): The object type, which is always `audio.voice`. Enum: 'audio.voice'.
- `id` (string, required): The voice identifier, which can be referenced in API endpoints.
- `name` (string, required): The name of the voice.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the voice was created.
