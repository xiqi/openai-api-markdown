# Stream Event (speech.audio.delta)

Source: https://platform.openai.com/docs/api-reference/audio/speech-audio-delta-event

Emitted for each chunk of audio data generated during speech synthesis.

## Properties
- `type` (string, required): The type of the event. Always `speech.audio.delta`. Enum: 'speech.audio.delta'.
- `audio` (string, required): A chunk of Base64-encoded audio data.
