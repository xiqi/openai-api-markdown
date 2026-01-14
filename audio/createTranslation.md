# Create translation

Source: https://platform.openai.com/docs/api-reference/audio/createTranslation

`POST /v1/audio/translations`

Translates audio into English.

## Request body
### multipart/form-data
- `file` (string, required): The audio file object (not file name) translate, in one of these formats: flac, mp3, mp4, mpeg, mpga, m4a, ogg, wav, or webm.
- `model` (string, required): ID of the model to use. Only `whisper-1` (which is powered by our open source Whisper V2 model) is currently available.
- `prompt` (string, optional): An optional text to guide the model's style or continue a previous audio segment. The [prompt](https://platform.openai.com/docs/guides/speech-to-text#prompting) should be in English.
- `response_format` (string, optional): The format of the output, in one of these options: `json`, `text`, `srt`, `verbose_json`, or `vtt`. Enum: 'json', 'text', 'srt', 'verbose_json', 'vtt'. Default: `json`.
- `temperature` (number, optional): The sampling temperature, between 0 and 1. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic. If set to 0, the model will use [log probability](https://en.wikipedia.org/wiki/Log_probability) to automatically increase the temperature until certain thresholds are hit. Default: `0`.

## Responses
### 200
OK
#### application/json
- Schema type: `object`

## Returns
The translated text.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/audio/translations \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: multipart/form-data" \
  -F file="@/path/to/file/german.m4a" \
  -F model="whisper-1"
```
#### Request (javascript)
```javascript
import fs from "fs";
import OpenAI from "openai";

const openai = new OpenAI();

async function main() {
    const translation = await openai.audio.translations.create({
        file: fs.createReadStream("speech.mp3"),
        model: "whisper-1",
    });

    console.log(translation.text);
}
main();
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

audio_file = open("speech.mp3", "rb")
transcript = client.audio.translations.create(
  model="whisper-1",
  file=audio_file
)
```
#### Request (csharp)
```csharp
using System;

using OpenAI.Audio;

string audioFilePath = "audio.mp3";

AudioClient client = new(
    model: "whisper-1",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

AudioTranscription transcription = client.TranscribeAudio(audioFilePath);

Console.WriteLine($"{transcription.Text}");
```
#### Response
```json
{
  "text": "Hello, my name is Wolfgang and I come from Germany. Where are you heading today?"
}
```
