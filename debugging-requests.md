# Debugging requests

Source: https://platform.openai.com/docs/api-reference/debugging-requests

In addition to [error codes](https://platform.openai.com/docs/guides/error-codes) returned from API responses, you can inspect HTTP response headers containing the unique ID of a particular API request or information about rate limiting applied to your requests. Below is an incomplete list of HTTP headers returned with API responses:

**API meta information**
* `openai-organization`: The [organization](https://platform.openai.com/docs/guides/production-best-practices#setting-up-your-organization) associated with the request
* `openai-processing-ms`: Time taken processing your API request
* `openai-version`: REST API version used for this request (currently `2020-10-01`)
* `x-request-id`: Unique identifier for this API request (used in troubleshooting)

**[Rate limiting information](https://platform.openai.com/docs/guides/rate-limits)**
* `x-ratelimit-limit-requests`
* `x-ratelimit-limit-tokens`
* `x-ratelimit-remaining-requests`
* `x-ratelimit-remaining-tokens`
* `x-ratelimit-reset-requests`
* `x-ratelimit-reset-tokens`

**OpenAI recommends logging request IDs in production deployments** for more efficient troubleshooting with our [support team](https://help.openai.com/en/), should the need arise. Our [official SDKs](https://platform.openai.com/docs/libraries) provide a property on top-level response objects containing the value of the `x-request-id` header. 

### Supplying your own request ID with `X-Client-Request-Id`

In addition to the server-generated `x-request-id`, you can supply your own unique identifier for each request via the `X-Client-Request-Id` request header. This header is not added automatically; you must explicitly set it on the request.

When you include `X-Client-Request-Id`:

* You control the ID format (for example, a UUID or your internal trace ID), but it must contain only ASCII characters and be no more than 512 characters long; otherwise, the request will fail with a 400 error. We strongly recommend making this value unique per request.

* OpenAI will log this value in our internal logs for supported endpoints, including chat/completions, embeddings, responses, and more.

* In cases like timeouts or network issues when you can’t get the `X-Request-Id` response header, you can share the `X-Client-Request-Id` value with our support team, and we can look up whether we received the request and when.

**Example:**

```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "X-Client-Request-Id: 123e4567-e89b-12d3-a456-426614174000"
```
