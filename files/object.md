# The file object

Source: https://platform.openai.com/docs/api-reference/files/object

The `File` object represents a document that has been uploaded to OpenAI.

## Properties
- `id` (string, required): The file identifier, which can be referenced in the API endpoints.
- `bytes` (integer, required): The size of the file, in bytes.
- `created_at` (integer, required): The Unix timestamp (in seconds) for when the file was created.
- `expires_at` (integer, optional): The Unix timestamp (in seconds) for when the file will expire.
- `filename` (string, required): The name of the file.
- `object` (string, required): The object type, which is always `file`. Enum: 'file'.
- `purpose` (string, required): The intended purpose of the file. Supported values are `assistants`, `assistants_output`, `batch`, `batch_output`, `fine-tune`, `fine-tune-results`, `vision`, and `user_data`. Enum: 'assistants', 'assistants_output', 'batch', 'batch_output', 'fine-tune', 'fine-tune-results', 'vision', 'user_data'.
- `status` (string, required): Deprecated. The current status of the file, which can be either `uploaded`, `processed`, or `error`. Enum: 'uploaded', 'processed', 'error'. Deprecated.
- `status_details` (string, optional): Deprecated. For details on why a fine-tuning training file failed validation, see the `error` field on `fine_tuning.job`. Deprecated.
