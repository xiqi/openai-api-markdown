# Create speech

Source: https://platform.openai.com/docs/api-reference/audio/createSpeech

`POST /v1/audio/speech`

Generates audio from the input text.

## Request body
### application/json
- `model` (string, required): One of the available [TTS models](https://platform.openai.com/docs/models#tts): `tts-1`, `tts-1-hd`, `gpt-4o-mini-tts`, or `gpt-4o-mini-tts-2025-12-15`.
- `input` (string, required): The text to generate audio for. The maximum length is 4096 characters.
- `instructions` (string, optional): Control the voice of your generated audio with additional instructions. Does not work with `tts-1` or `tts-1-hd`.
- `voice` (string | object, required): The voice to use when generating the audio. Supported built-in voices are `alloy`, `ash`, `ballad`, `coral`, `echo`, `fable`, `onyx`, `nova`, `sage`, `shimmer`, `verse`, `marin`, and `cedar`. You may also provide a custom voice object with an `id`, for example `{ "id": "voice_1234" }`. Previews of the voices are available in the [Text to speech guide](https://platform.openai.com/docs/guides/text-to-speech#voice-options).
  - Variant (object):
    - `id` (string, required): The custom voice ID, e.g. `voice_1234`.
- `response_format` (string, optional): The format to audio in. Supported formats are `mp3`, `opus`, `aac`, `flac`, `wav`, and `pcm`. Enum: 'mp3', 'opus', 'aac', 'flac', 'wav', 'pcm'. Default: `mp3`.
- `speed` (number, optional): The speed of the generated audio. Select a value from `0.25` to `4.0`. `1.0` is the default. Default: `1`.
- `stream_format` (string, optional): The format to stream the audio in. Supported formats are `sse` and `audio`. `sse` is not supported for `tts-1` or `tts-1-hd`. Enum: 'sse', 'audio'. Default: `audio`.

## Responses
### 200
OK
#### application/octet-stream
- Schema type: `string`
#### text/event-stream
- Schema type: `object`

## Returns
The audio file content or a [stream of audio events](speech-audio-delta-event.md).

## Examples
### Default
#### Request (curl)
```bash
curl https://api.openai.com/v1/audio/speech \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-mini-tts",
    "input": "The quick brown fox jumped over the lazy dog.",
    "voice": "alloy"
  }' \
  --output speech.mp3
```
#### Request (javascript)
```javascript
import fs from "fs";
import path from "path";
import OpenAI from "openai";

const openai = new OpenAI();

const speechFile = path.resolve("./speech.mp3");

async function main() {
  const mp3 = await openai.audio.speech.create({
    model: "gpt-4o-mini-tts",
    voice: "alloy",
    input: "Today is a wonderful day to build something people love!",
  });
  console.log(speechFile);
  const buffer = Buffer.from(await mp3.arrayBuffer());
  await fs.promises.writeFile(speechFile, buffer);
}
main();
```
#### Request (python)
```python
from pathlib import Path
import openai

speech_file_path = Path(__file__).parent / "speech.mp3"
with openai.audio.speech.with_streaming_response.create(
  model="gpt-4o-mini-tts",
  voice="alloy",
  input="The quick brown fox jumped over the lazy dog."
) as response:
  response.stream_to_file(speech_file_path)
```
#### Request (csharp)
```csharp
using System;
using System.IO;

using OpenAI.Audio;

AudioClient client = new(
    model: "gpt-4o-mini-tts",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

BinaryData speech = client.GenerateSpeech(
    text: "The quick brown fox jumped over the lazy dog.",
    voice: GeneratedSpeechVoice.Alloy
);

using FileStream stream = File.OpenWrite("speech.mp3");
speech.ToStream().CopyTo(stream);
```
### SSE Stream Format
#### Request (curl)
```bash
curl https://api.openai.com/v1/audio/speech \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o-mini-tts",
    "input": "The quick brown fox jumped over the lazy dog.",
    "voice": "alloy",
    "stream_format": "sse"
  }'
```
