# Cancel chat session

Source: https://platform.openai.com/docs/api-reference/chatkit/sessions/cancel

`POST /v1/chatkit/sessions/{session_id}/cancel`

Cancel a ChatKit session

## Parameters
- `session_id` (path, string, required): Unique identifier for the ChatKit session to cancel.

## Responses
### 200
Success
#### application/json
- `id` (string, required): Identifier for the ChatKit session.
- `object` (string, required): Type discriminator that is always `chatkit.session`. Enum: 'chatkit.session'. Default: `chatkit.session`.
- `expires_at` (integer, required): Unix timestamp (in seconds) for when the session expires.
- `client_secret` (string, required): Ephemeral client secret that authenticates session requests.
- `workflow` (object, required): Workflow metadata for the session.
  - `id` (string, required): Identifier of the workflow backing the session.
  - `version` (string | null, required)
  - `state_variables` (object | null, required)
  - `tracing` (object, required): Tracing settings applied to the workflow.
    - `enabled` (boolean, required): Indicates whether tracing is enabled.
- `user` (string, required): User identifier associated with the session.
- `rate_limits` (object, required): Resolved rate limit values.
  - `max_requests_per_1_minute` (integer, required): Maximum allowed requests per one-minute window.
- `max_requests_per_1_minute` (integer, required): Convenience copy of the per-minute request limit.
- `status` (string, required): Current lifecycle state of the session. Enum: 'active', 'expired', 'cancelled'.
- `chatkit_configuration` (object, required): Resolved ChatKit feature configuration for the session.
  - `automatic_thread_titling` (object, required): Automatic thread titling preferences.
    - `enabled` (boolean, required): Whether automatic thread titling is enabled.
  - `file_upload` (object, required): Upload settings for the session.
    - `enabled` (boolean, required): Indicates if uploads are enabled for the session.
    - `max_file_size` (integer | null, required)
    - `max_files` (integer | null, required)
  - `history` (object, required): History retention configuration.
    - `enabled` (boolean, required): Indicates if chat history is persisted for the session.
    - `recent_threads` (integer | null, required)

Example:
```json
{
  "id": "cksess_123",
  "object": "chatkit.session",
  "client_secret": "ek_token_123",
  "expires_at": 1712349876,
  "workflow": {
    "id": "workflow_alpha",
    "version": "2024-10-01"
  },
  "user": "user_789",
  "rate_limits": {
    "max_requests_per_1_minute": 60
  },
  "max_requests_per_1_minute": 60,
  "status": "cancelled",
  "chatkit_configuration": {
    "automatic_thread_titling": {
      "enabled": true
    },
    "file_upload": {
      "enabled": true,
      "max_file_size": 16,
      "max_files": 20
    },
    "history": {
      "enabled": true,
      "recent_threads": 10
    }
  }
}
```

## Returns
Returns the chat session after it has been cancelled. Cancelling prevents new requests from using the issued client secret.

## Examples
### Cancel a ChatKit session by ID
#### Request (curl)
```bash
curl -X POST \
  https://api.openai.com/v1/chatkit/sessions/cksess_123/cancel \
  -H "OpenAI-Beta: chatkit_beta=v1" \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (javascript)
```javascript
import OpenAI from 'openai';

const client = new OpenAI();

const chatSession = await client.beta.chatkit.sessions.cancel('cksess_123');

console.log(chatSession.id);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
chat_session = client.beta.chatkit.sessions.cancel(
    "cksess_123",
)
print(chat_session.id)
```
#### Response
```json
{
  "id": "cksess_123",
  "object": "chatkit.session",
  "workflow": {
    "id": "workflow_alpha",
    "version": "1"
  },
  "scope": {
    "customer_id": "cust_456"
  },
  "max_requests_per_1_minute": 30,
  "ttl_seconds": 900,
  "status": "cancelled",
  "cancelled_at": 1712345678
}
```
