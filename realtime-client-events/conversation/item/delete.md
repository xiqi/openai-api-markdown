# conversation.item.delete

Source: https://platform.openai.com/docs/api-reference/realtime-client-events/conversation/item/delete

Send this event when you want to remove any item from the conversation 
history. The server will respond with a `conversation.item.deleted` event, 
unless the item does not exist in the conversation history, in which case the 
server will respond with an error.

## Properties
- `event_id` (string, optional): Optional client-generated ID used to identify this event.
- `type` (string, required): The event type, must be `conversation.item.delete`. Enum: 'conversation.item.delete'.
- `item_id` (string, required): The ID of the item to delete.
