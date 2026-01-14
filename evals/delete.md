# Delete an eval

Source: https://platform.openai.com/docs/api-reference/evals/delete

`DELETE /v1/evals/{eval_id}`

Delete an evaluation.

## Parameters
- `eval_id` (path, string, required): The ID of the evaluation to delete.

## Responses
### 200
Successfully deleted the evaluation.
#### application/json
- `object` (string, required)
- `deleted` (boolean, required)
- `eval_id` (string, required)
### 404
Evaluation not found.
#### application/json
- `code` (string | null, required)
- `message` (string, required)
- `param` (string | null, required)
- `type` (string, required)

## Returns
A deletion confirmation object.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/evals/eval_abc123 \
  -X DELETE \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

deleted = client.evals.delete("eval_abc123")
print(deleted)
```
#### Response
```json
{
  "object": "eval.deleted",
  "deleted": true,
  "eval_id": "eval_abc123"
}
```
