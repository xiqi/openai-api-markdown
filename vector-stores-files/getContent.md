# Retrieve vector store file content

Source: https://platform.openai.com/docs/api-reference/vector-stores-files/getContent

`GET /v1/vector_stores/{vector_store_id}/files/{file_id}/content`

Retrieve the parsed contents of a vector store file.

## Parameters
- `vector_store_id` (path, string, required): The ID of the vector store.
- `file_id` (path, string, required): The ID of the file within the vector store.

## Responses
### 200
OK
#### application/json
- `object` (string, required): The object type, which is always `vector_store.file_content.page` Enum: 'vector_store.file_content.page'.
- `data` (array<object>, required): Parsed content of the file.
  - Items:
    - `type` (string, optional): The content type (currently only `"text"`)
    - `text` (string, optional): The text content
- `has_more` (boolean, required): Indicates if there are more content pages to fetch.
- `next_page` (string | null, required)

## Returns
The parsed contents of the specified vector store file.

## Examples
### Example
#### Request (curl)
```bash
curl \
https://api.openai.com/v1/vector_stores/vs_abc123/files/file-abc123/content \
-H "Authorization: Bearer $OPENAI_API_KEY"
```
#### Response
```json
{
  "file_id": "file-abc123",
  "filename": "example.txt",
  "attributes": {"key": "value"},
  "content": [
    {"type": "text", "text": "..."},
    ...
  ]
}
```
