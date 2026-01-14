# Client secrets

Source: https://platform.openai.com/docs/api-reference/realtime-sessions

REST API endpoint to generate ephemeral client secrets for use in client-side
applications. Client secrets are short-lived tokens that can be passed to a client app,
such as a web frontend or mobile client, which grants access to the Realtime API without
leaking your main API key. You can configure a custom TTL for each client secret.

You can also attach session configuration options to the client secret, which will be
applied to any sessions created using that client secret, but these can also be overridden
by the client connection.

[Learn more about authentication with client secrets over WebRTC](https://platform.openai.com/docs/guides/realtime-webrtc).

## Contents
- [Create client secret](create-realtime-client-secret.md)
- [Session response object](create-secret-response.md)
