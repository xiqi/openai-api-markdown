# The message delta object

Source: https://platform.openai.com/docs/api-reference/assistants-streaming/message-delta-object

Represents a message delta i.e. any changed fields on a message during streaming.

## Properties
- `id` (string, required): The identifier of the message, which can be referenced in API endpoints.
- `object` (string, required): The object type, which is always `thread.message.delta`. Enum: 'thread.message.delta'.
- `delta` (object, required): The delta containing the fields that have changed on the Message.
  - `role` (string, optional): The entity that produced the message. One of `user` or `assistant`. Enum: 'user', 'assistant'.
  - `content` (array<object>, optional): The content of the message in array of text and/or images.
