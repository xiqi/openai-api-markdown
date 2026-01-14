# List fine-tuning events

Source: https://platform.openai.com/docs/api-reference/fine-tuning/list-events

`GET /v1/fine_tuning/jobs/{fine_tuning_job_id}/events`

Get status updates for a fine-tuning job.

## Parameters
- `fine_tuning_job_id` (path, string, required): The ID of the fine-tuning job to get events for.
- `after` (query, string, optional): Identifier for the last event from the previous pagination request.
- `limit` (query, integer, optional): Number of events to retrieve. Default: `20`.

## Responses
### 200
OK
#### application/json
- `data` (array<object>, required)
  - Items:
    - `object` (string, required): The object type, which is always "fine_tuning.job.event". Enum: 'fine_tuning.job.event'.
    - `id` (string, required): The object identifier.
    - `created_at` (integer, required): The Unix timestamp (in seconds) for when the fine-tuning job was created.
    - `level` (string, required): The log level of the event. Enum: 'info', 'warn', 'error'.
    - `message` (string, required): The message of the event.
    - `type` (string, optional): The type of event. Enum: 'message', 'metrics'.
    - `data` (object, optional): The data associated with the event.
- `object` (string, required) Enum: 'list'.
- `has_more` (boolean, required)

## Returns
A list of fine-tuning event objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/fine_tuning/jobs/ftjob-abc123/events \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.fine_tuning.jobs.list_events(
  fine_tuning_job_id="ftjob-abc123",
  limit=2
)
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "object": "fine_tuning.job.event",
      "id": "ft-event-ddTJfwuMVpfLXseO0Am0Gqjm",
      "created_at": 1721764800,
      "level": "info",
      "message": "Fine tuning job successfully completed",
      "data": null,
      "type": "message"
    },
    {
      "object": "fine_tuning.job.event",
      "id": "ft-event-tyiGuB72evQncpH87xe505Sv",
      "created_at": 1721764800,
      "level": "info",
      "message": "New fine-tuned model created: ft:gpt-4o-mini:openai::7p4lURel",
      "data": null,
      "type": "message"
    }
  ],
  "has_more": true
}
```
