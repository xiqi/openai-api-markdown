# Backward compatibility

Source: https://platform.openai.com/docs/api-reference/backward-compatibility

OpenAI is committed to providing stability to API users by avoiding breaking changes in major API versions whenever reasonably possible. This includes:

- The REST API (currently `v1`)
- Our first-party [SDKs](https://platform.openai.com/docs/libraries) (released SDKs adhere to [semantic versioning](https://semver.org/))
- [Model](https://platform.openai.com/docs/models) families (like `gpt-4o` or `o4-mini`)

**Model prompting behavior between snapshots is subject to change**.
Model outputs are by their nature variable, so expect changes in prompting and model behavior between snapshots. For example, if you moved from `gpt-4o-2024-05-13` to `gpt-4o-2024-08-06`, the same `system` or `user` messages could function differently between versions. The best way to ensure consistent prompting behavior and model output is to use pinned model versions, and to implement [evals](https://platform.openai.com/docs/guides/evals) for your applications.

**Backwards-compatible API changes**:
- Adding new resources (URLs) to the REST API and SDKs
- Adding new optional API parameters
- Adding new properties to JSON response objects or event data
- Changing the order of properties in a JSON response object
- Changing the length or format of opaque strings, like resource identifiers and UUIDs
- Adding new event types (in either streaming or the Realtime API)

See the [changelog](https://platform.openai.com/docs/changelog) for a list of backwards-compatible changes and rare breaking changes.
