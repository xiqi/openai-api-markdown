# Realtime Beta client events

Source: https://platform.openai.com/docs/api-reference/realtime-beta-client-events

These are events that the OpenAI Realtime WebSocket server will accept from the client.

## Contents
- [session](session.md)
  - [session.update](session/update.md)
- [input_audio_buffer](input_audio_buffer.md)
  - [input_audio_buffer.append](input_audio_buffer/append.md)
  - [input_audio_buffer.commit](input_audio_buffer/commit.md)
  - [input_audio_buffer.clear](input_audio_buffer/clear.md)
- [conversation](conversation.md)
  - [.item](conversation/item.md)
    - [conversation.item.create](conversation/item/create.md)
    - [conversation.item.retrieve](conversation/item/retrieve.md)
    - [conversation.item.truncate](conversation/item/truncate.md)
    - [conversation.item.delete](conversation/item/delete.md)
- [response](response.md)
  - [response.create](response/create.md)
  - [response.cancel](response/cancel.md)
- [transcription_session](transcription_session.md)
  - [transcription_session.update](transcription_session/update.md)
- [output_audio_buffer](output_audio_buffer.md)
  - [output_audio_buffer.clear](output_audio_buffer/clear.md)
