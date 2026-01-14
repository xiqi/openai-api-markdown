# The fine-tuning job event object

Source: https://platform.openai.com/docs/api-reference/fine-tuning/event-object

Fine-tuning job event object

## Properties
- `object` (string, required): The object type, which is always "fine_tuning.job.event". Enum: 'fine_tuning.job.event'.
- `id` (string, required): The object identifier.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the fine-tuning job was created.
- `level` (string, required): The log level of the event. Enum: 'info', 'warn', 'error'.
- `message` (string, required): The message of the event.
- `type` (string, optional): The type of event. Enum: 'message', 'metrics'.
- `data` (object, optional): The data associated with the event.
