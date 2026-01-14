# The voice consent list object

Source: https://platform.openai.com/docs/api-reference/audio/voice-consent-list

## Properties
- `object` (string, required) Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `object` (string, required): The object type, which is always `audio.voice_consent`. Enum: 'audio.voice_consent'.
    - `id` (string, required): The consent recording identifier.
    - `name` (string, required): The label provided when the consent recording was uploaded.
    - `language` (string, required): The BCP 47 language tag for the consent phrase (for example, `en-US`).
    - `created_at` (integer, required): The Unix timestamp (in seconds) for when the consent recording was created.
- `first_id` (string | null, optional)
- `last_id` (string | null, optional)
- `has_more` (boolean, required)
