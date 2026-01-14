# response.output_audio_transcript.done

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/response/output_audio_transcript/done

Returned when the model-generated transcription of audio output is done
streaming. Also emitted when a Response is interrupted, incomplete, or
cancelled.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `response.output_audio_transcript.done`. Enum: 'response.output_audio_transcript.done'.
- `response_id` (string, required): The ID of the response.
- `item_id` (string, required): The ID of the item.
- `output_index` (integer, required): The index of the output item in the response.
- `content_index` (integer, required): The index of the content part in the item's content array.
- `transcript` (string, required): The final transcript of the audio.
