# conversation.item.deleted

Source: https://platform.openai.com/docs/api-reference/realtime-server-events/conversation/item/deleted

Returned when an item in the conversation is deleted by the client with a 
`conversation.item.delete` event. This event is used to synchronize the 
server's understanding of the conversation history with the client's view.

## Properties
- `event_id` (string, required): The unique ID of the server event.
- `type` (string, required): The event type, must be `conversation.item.deleted`. Enum: 'conversation.item.deleted'.
- `item_id` (string, required): The ID of the item that was deleted.
