# Authentication

Source: https://platform.openai.com/docs/api-reference/authentication

The OpenAI API uses API keys for authentication. Create, manage, and learn more about API keys in your [organization settings](https://platform.openai.com/settings/organization/api-keys).

**Remember that your API key is a secret!** Do not share it with others or expose it in any client-side code (browsers, apps). API keys should be securely loaded from an environment variable or key management service on the server.

API keys should be provided via [HTTP Bearer authentication](https://swagger.io/docs/specification/v3_0/authentication/bearer-authentication/).

```bash
Authorization: Bearer OPENAI_API_KEY
```



If you belong to multiple organizations or access projects through a legacy user API key, pass a header to specify which organization and project to use for an API request:

```bash
curl https://api.openai.com/v1/models \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "OpenAI-Organization: $ORGANIZATION_ID" \
  -H "OpenAI-Project: $PROJECT_ID"
```

Usage from these API requests counts as usage for the specified organization and project.Organization IDs can be found on your [organization settings](https://platform.openai.com/settings/organization/general) page.
Project IDs can be found on your [general settings](https://platform.openai.com/settings) page by selecting the specific project.
