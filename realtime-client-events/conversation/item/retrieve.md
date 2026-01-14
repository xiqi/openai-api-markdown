# conversation.item.retrieve

Source: https://platform.openai.com/docs/api-reference/realtime-client-events/conversation/item/retrieve

Send this event when you want to retrieve the server's representation of a specific item in the conversation history. This is useful, for example, to inspect user audio after noise cancellation and VAD.
The server will respond with a `conversation.item.retrieved` event, 
unless the item does not exist in the conversation history, in which case the 
server will respond with an error.

## Properties
- `event_id` (string, optional): Optional client-generated ID used to identify this event.
- `type` (string, required): The event type, must be `conversation.item.retrieve`. Enum: 'conversation.item.retrieve'.
- `item_id` (string, required): The ID of the item to retrieve.
