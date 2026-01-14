# Streaming

Source: https://platform.openai.com/docs/api-reference/assistants-streaming

Stream the result of executing a Run or resuming a Run after submitting tool outputs.
You can stream events from the [Create Thread and Run](../runs/createThreadAndRun.md),
[Create Run](../runs/createRun.md), and [Submit Tool Outputs](../runs/submitToolOutputs.md)
endpoints by passing `"stream": true`. The response will be a [Server-Sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events) stream.
Our Node and Python SDKs provide helpful utilities to make streaming easy. Reference the
[Assistants API quickstart](https://platform.openai.com/docs/assistants/overview) to learn more.

## Contents
- [The message delta object](message-delta-object.md)
- [The run step delta object](run-step-delta-object.md)
- [Assistant stream events](events.md)
