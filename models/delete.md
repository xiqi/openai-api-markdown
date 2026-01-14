# Delete a fine-tuned model

Source: https://platform.openai.com/docs/api-reference/models/delete

`DELETE /v1/models/{model}`

Delete a fine-tuned model. You must have the Owner role in your organization to delete a model.

## Parameters
- `model` (path, string, required): The model to delete

## Responses
### 200
OK
#### application/json
- `id` (string, required)
- `deleted` (boolean, required)
- `object` (string, required)

## Returns
Deletion status.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/models/ft:gpt-4o-mini:acemeco:suffix:abc123 \
  -X DELETE \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

client.models.delete("ft:gpt-4o-mini:acemeco:suffix:abc123")
```
#### Request (csharp)
```csharp
using System;
using System.ClientModel;

using OpenAI.Models;

OpenAIModelClient client = new(
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

ClientResult success = client.DeleteModel("ft:gpt-4o-mini:acemeco:suffix:abc123");
Console.WriteLine(success);
```
#### Response
```json
{
  "id": "ft:gpt-4o-mini:acemeco:suffix:abc123",
  "object": "model",
  "deleted": true
}
```
