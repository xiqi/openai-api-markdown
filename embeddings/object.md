# The embedding object

Source: https://platform.openai.com/docs/api-reference/embeddings/object

Represents an embedding vector returned by embedding endpoint.

## Properties
- `index` (integer, required): The index of the embedding in the list of embeddings.
- `embedding` (array<number>, required): The embedding vector, which is a list of floats. The length of vector depends on the model as listed in the [embedding guide](https://platform.openai.com/docs/guides/embeddings).
- `object` (string, required): The object type, which is always "embedding". Enum: 'embedding'.
