# Webhook Events

Source: https://platform.openai.com/docs/api-reference/webhook-events

Webhooks are HTTP requests sent by OpenAI to a URL you specify when certain
events happen during the course of API usage.

[Learn more about webhooks](https://platform.openai.com/docs/guides/webhooks).

## Contents
- [response](response.md)
  - [response.completed](response/completed.md)
  - [response.cancelled](response/cancelled.md)
  - [response.failed](response/failed.md)
  - [response.incomplete](response/incomplete.md)
- [batch](batch.md)
  - [batch.completed](batch/completed.md)
  - [batch.cancelled](batch/cancelled.md)
  - [batch.expired](batch/expired.md)
  - [batch.failed](batch/failed.md)
- [fine_tuning](fine_tuning.md)
  - [.job](fine_tuning/job.md)
    - [fine_tuning.job.succeeded](fine_tuning/job/succeeded.md)
    - [fine_tuning.job.failed](fine_tuning/job/failed.md)
    - [fine_tuning.job.cancelled](fine_tuning/job/cancelled.md)
- [eval](eval.md)
  - [.run](eval/run.md)
    - [eval.run.succeeded](eval/run/succeeded.md)
    - [eval.run.failed](eval/run/failed.md)
    - [eval.run.canceled](eval/run/canceled.md)
- [realtime](realtime.md)
  - [.call](realtime/call.md)
    - [realtime.call.incoming](realtime/call/incoming.md)
