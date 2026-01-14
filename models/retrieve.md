# Retrieve model

Source: https://platform.openai.com/docs/api-reference/models/retrieve

`GET /v1/models/{model}`

Retrieves a model instance, providing basic information about the model such as the owner and permissioning.

## Parameters
- `model` (path, string, required): The ID of the model to use for this request

## Responses
### 200
OK
#### application/json
- `id` (string, required): The model identifier, which can be referenced in the API endpoints.
- `created` (integer, required): The Unix timestamp (in seconds) when the model was created.
- `object` (string, required): The object type, which is always "model". Enum: 'model'.
- `owned_by` (string, required): The organization that owns the model.

## Returns
The [model](object.md) object matching the specified ID.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/models/VAR_chat_model_id \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.models.retrieve("VAR_chat_model_id")
```
#### Request (csharp)
```csharp
using System;
using System.ClientModel;

using OpenAI.Models;

  OpenAIModelClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

ClientResult<OpenAIModel> model = client.GetModel("babbage-002");
Console.WriteLine(model.Value.Id);
```
#### Response
```json
{
  "id": "VAR_chat_model_id",
  "object": "model",
  "created": 1686935002,
  "owned_by": "openai"
}
```
