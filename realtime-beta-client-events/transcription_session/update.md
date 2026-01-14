# transcription_session.update

Source: https://platform.openai.com/docs/api-reference/realtime-beta-client-events/transcription_session/update

Send this event to update a transcription session.

## Properties
- `event_id` (string, optional): Optional client-generated ID used to identify this event.
- `type` (string, required): The event type, must be `transcription_session.update`. Enum: 'transcription_session.update'.
- `session` (object, required): Realtime transcription session object configuration.
  - `turn_detection` (object, optional): Configuration for turn detection. Can be set to `null` to turn off. Server VAD means that the model will detect the start and end of speech based on audio volume and respond at the end of user speech.
    - `type` (string, optional): Type of turn detection. Only `server_vad` is currently supported for transcription sessions. Enum: 'server_vad'.
    - `threshold` (number, optional): Activation threshold for VAD (0.0 to 1.0), this defaults to 0.5. A
      higher threshold will require louder audio to activate the model, and
      thus might perform better in noisy environments.
    - `prefix_padding_ms` (integer, optional): Amount of audio to include before the VAD detected speech (in
      milliseconds). Defaults to 300ms.
    - `silence_duration_ms` (integer, optional): Duration of silence to detect speech stop (in milliseconds). Defaults
      to 500ms. With shorter values the model will respond more quickly,
      but may jump in on short pauses from the user.
  - `input_audio_noise_reduction` (object, optional): Configuration for input audio noise reduction. This can be set to `null` to turn off.
    Noise reduction filters audio added to the input audio buffer before it is sent to VAD and the model.
    Filtering the audio can improve VAD and turn detection accuracy (reducing false positives) and model performance by improving perception of the input audio.
    - `type` (string, optional): Type of noise reduction. `near_field` is for close-talking microphones such as headphones, `far_field` is for far-field microphones such as laptop or conference room microphones. Enum: 'near_field', 'far_field'.
  - `input_audio_format` (string, optional): The format of input audio. Options are `pcm16`, `g711_ulaw`, or `g711_alaw`.
    For `pcm16`, input audio must be 16-bit PCM at a 24kHz sample rate,
    single channel (mono), and little-endian byte order. Enum: 'pcm16', 'g711_ulaw', 'g711_alaw'. Default: `pcm16`.
  - `input_audio_transcription` (object, optional): Configuration for input audio transcription. The client can optionally set the language and prompt for transcription, these offer additional guidance to the transcription service.
    - `model` (string, optional): The model to use for transcription. Current options are `whisper-1`, `gpt-4o-mini-transcribe`, `gpt-4o-mini-transcribe-2025-12-15`, `gpt-4o-transcribe`, and `gpt-4o-transcribe-diarize`. Use `gpt-4o-transcribe-diarize` when you need diarization with speaker labels.
    - `language` (string, optional): The language of the input audio. Supplying the input language in
      [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) (e.g. `en`) format
      will improve accuracy and latency.
    - `prompt` (string, optional): An optional text to guide the model's style or continue a previous audio
      segment.
      For `whisper-1`, the [prompt is a list of keywords](https://platform.openai.com/docs/guides/speech-to-text#prompting).
      For `gpt-4o-transcribe` models (excluding `gpt-4o-transcribe-diarize`), the prompt is a free text string, for example "expect words related to technology".
  - `include` (array<string>, optional): The set of items to include in the transcription. Current available items are:
    `item.input_audio_transcription.logprobs`
