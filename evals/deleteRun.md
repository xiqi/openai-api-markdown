# Delete eval run

Source: https://platform.openai.com/docs/api-reference/evals/deleteRun

`DELETE /v1/evals/{eval_id}/runs/{run_id}`

Delete an eval run.

## Parameters
- `eval_id` (path, string, required): The ID of the evaluation to delete the run from.
- `run_id` (path, string, required): The ID of the run to delete.

## Responses
### 200
Successfully deleted the eval run
#### application/json
- `object` (string, optional)
- `deleted` (boolean, optional)
- `run_id` (string, optional)
### 404
Run not found
#### application/json
- `code` (string | null, required)
- `message` (string, required)
- `param` (string | null, required)
- `type` (string, required)

## Returns
An object containing the status of the delete operation.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/evals/eval_123abc/runs/evalrun_abc456 \
  -X DELETE \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json"
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

deleted = client.evals.runs.delete(
  "eval_123abc",
  "evalrun_abc456"
)
print(deleted)
```
#### Response
```json
{
  "object": "eval.run.deleted",
  "deleted": true,
  "run_id": "evalrun_abc456"
}
```
