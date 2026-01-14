# Create ChatKit session

Source: https://platform.openai.com/docs/api-reference/chatkit/sessions/create

`POST /v1/chatkit/sessions`

Create a ChatKit session

## Request body
### application/json
- `workflow` (object, required): Workflow that powers the session.
  - `id` (string, required): Identifier for the workflow invoked by the session.
  - `version` (string, optional): Specific workflow version to run. Defaults to the latest deployed version.
  - `state_variables` (object, optional): State variables forwarded to the workflow. Keys may be up to 64 characters, values must be primitive types, and the map defaults to an empty object.
  - `tracing` (object, optional): Optional tracing overrides for the workflow invocation. When omitted, tracing is enabled by default.
    - `enabled` (boolean, optional): Whether tracing is enabled during the session. Defaults to true.
- `user` (string, required): A free-form string that identifies your end user; ensures this Session can access other objects that have the same `user` scope.
- `expires_after` (object, optional): Optional override for session expiration timing in seconds from creation. Defaults to 10 minutes.
  - `anchor` (string, required): Base timestamp used to calculate expiration. Currently fixed to `created_at`. Enum: 'created_at'. Default: `created_at`.
  - `seconds` (integer, required): Number of seconds after the anchor when the session expires.
- `rate_limits` (object, optional): Optional override for per-minute request limits. When omitted, defaults to 10.
  - `max_requests_per_1_minute` (integer, optional): Maximum number of requests allowed per minute for the session. Defaults to 10.
- `chatkit_configuration` (object, optional): Optional overrides for ChatKit runtime configuration features
  - `automatic_thread_titling` (object, optional): Configuration for automatic thread titling. When omitted, automatic thread titling is enabled by default.
    - `enabled` (boolean, optional): Enable automatic thread title generation. Defaults to true.
  - `file_upload` (object, optional): Configuration for upload enablement and limits. When omitted, uploads are disabled by default (max_files 10, max_file_size 512 MB).
    - `enabled` (boolean, optional): Enable uploads for this session. Defaults to false.
    - `max_file_size` (integer, optional): Maximum size in megabytes for each uploaded file. Defaults to 512 MB, which is the maximum allowable size.
    - `max_files` (integer, optional): Maximum number of files that can be uploaded to the session. Defaults to 10.
  - `history` (object, optional): Configuration for chat history retention. When omitted, history is enabled by default with no limit on recent_threads (null).
    - `enabled` (boolean, optional): Enables chat users to access previous ChatKit threads. Defaults to true.
    - `recent_threads` (integer, optional): Number of recent ChatKit threads users have access to. Defaults to unlimited when unset.

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
Returns a [ChatKit session](object.md) object.

## Examples
### Create a scoped session
#### Request (curl)
```bash
curl https://api.openai.com/v1/chatkit/sessions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Beta: chatkit_beta=v1" \
  -d '{
    "workflow": {
      "id": "workflow_alpha",
      "version": "2024-10-01"
    },
    "scope": {
      "project": "alpha",
      "environment": "staging"
    },
    "expires_after": 1800,
    "max_requests_per_1_minute": 60,
    "max_requests_per_session": 500
  }'
```
#### Request (javascript)
```javascript
import OpenAI from 'openai';

const client = new OpenAI();

const chatSession = await client.beta.chatkit.sessions.create({ user: 'user', workflow: { id: 'id' } });

console.log(chatSession.id);
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()
chat_session = client.beta.chatkit.sessions.create(
    user="user",
    workflow={
        "id": "id"
    },
)
print(chat_session.id)
```
#### Response
```json
{
  "client_secret": "chatkit_token_123",
  "expires_at": 1735689600,
  "workflow": {
    "id": "workflow_alpha",
    "version": "2024-10-01"
  },
  "scope": {
    "project": "alpha",
    "environment": "staging"
  },
  "max_requests_per_1_minute": 60,
  "max_requests_per_session": 500,
  "status": "active"
}
```
