# List voice consents

Source: https://platform.openai.com/docs/api-reference/audio/listVoiceConsents

`GET /v1/audio/voice_consents`

Returns a list of voice consent recordings.

## Parameters
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.

## Responses
### 200
OK
#### application/json
- `object` (string, required) Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `object` (string, required): The object type, which is always `audio.voice_consent`. Enum: 'audio.voice_consent'.
    - `id` (string, required): The consent recording identifier.
    - `name` (string, required): The label provided when the consent recording was uploaded.
    - `language` (string, required): The BCP 47 language tag for the consent phrase (for example, `en-US`).
    - `created_at` (integer, required): The Unix timestamp (in seconds) for when the consent recording was created.
- `first_id` (string | null, optional)
- `last_id` (string | null, optional)
- `has_more` (boolean, required)

## Returns
A paginated list of voice consent recordings.

## Examples
### Default
#### Request (curl)
```bash
curl https://api.openai.com/v1/audio/voice_consents?limit=20 \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
