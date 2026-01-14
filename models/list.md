# List models

Source: https://platform.openai.com/docs/api-reference/models/list

`GET /v1/models`

Lists the currently available models, and provides basic information about each one such as the owner and availability.

## Responses
### 200
OK
#### application/json
- `object` (string, required) Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `id` (string, required): The model identifier, which can be referenced in the API endpoints.
    - `created` (integer, required): The Unix timestamp (in seconds) when the model was created.
    - `object` (string, required): The object type, which is always "model". Enum: 'model'.
    - `owned_by` (string, required): The organization that owns the model.

## Returns
A list of [model](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/models \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.models.list()
```
#### Request (csharp)
```csharp
using System;

using OpenAI.Models;

OpenAIModelClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

foreach (var model in client.GetModels().Value)
{
    Console.WriteLine(model.Id);
}
```
#### Response
```json
{
  "object": "list",
  "data": [
    {
      "id": "model-id-0",
      "object": "model",
      "created": 1686935002,
      "owned_by": "organization-owner"
    },
    {
      "id": "model-id-1",
      "object": "model",
      "created": 1686935002,
      "owned_by": "organization-owner",
    },
    {
      "id": "model-id-2",
      "object": "model",
      "created": 1686935002,
      "owned_by": "openai"
    },
  ]
}
```
