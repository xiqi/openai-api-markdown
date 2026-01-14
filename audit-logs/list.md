# List audit logs

Source: https://platform.openai.com/docs/api-reference/audit-logs/list

`GET /v1/organization/audit_logs`

List user actions and configuration changes within this organization.

## Parameters
- `effective_at` (query, object, optional): Return only events whose `effective_at` (Unix seconds) is in this range.
- `project_ids[]` (query, array<string>, optional): Return only events for these projects.
- `event_types[]` (query, array<string>, optional): Return only events with a `type` in one of these values. For example, `project.created`. For all options, see the documentation for the [audit log object](object.md).
- `actor_ids[]` (query, array<string>, optional): Return only events performed by these actors. Can be a user ID, a service account ID, or an api key tracking ID.
- `actor_emails[]` (query, array<string>, optional): Return only events performed by users with these emails.
- `resource_ids[]` (query, array<string>, optional): Return only events performed on these targets. For example, a project ID updated.
- `limit` (query, integer, optional): A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. Default: `20`.
- `after` (query, string, optional): A cursor for use in pagination. `after` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list.
- `before` (query, string, optional): A cursor for use in pagination. `before` is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, starting with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list.

## Responses
### 200
Audit logs listed successfully.
#### application/json
- `object` (string, required) Enum: 'list'.
- `data` (array<object>, required)
  - Items:
    - `id` (string, required): The ID of this log.
    - `type` (string, required): The event type. Enum: 'api_key.created', 'api_key.updated', 'api_key.deleted', 'certificate.created', 'certificate.updated', 'certificate.deleted', 'certificates.activated', 'certificates.deactivated', 'checkpoint.permission.created', 'checkpoint.permission.deleted', 'external_key.registered', 'external_key.removed', 'group.created', 'group.updated', 'group.deleted', 'invite.sent', 'invite.accepted', 'invite.deleted', 'ip_allowlist.created', 'ip_allowlist.updated', 'ip_allowlist.deleted', 'ip_allowlist.config.activated', 'ip_allowlist.config.deactivated', 'login.succeeded', 'login.failed', 'logout.succeeded', 'logout.failed', 'organization.updated', 'project.created', 'project.updated', 'project.archived', 'project.deleted', 'rate_limit.updated', 'rate_limit.deleted', 'resource.deleted', 'tunnel.created', 'tunnel.updated', 'tunnel.deleted', 'role.created', 'role.updated', 'role.deleted', 'role.assignment.created', 'role.assignment.deleted', 'scim.enabled', 'scim.disabled', 'service_account.created', 'service_account.updated', 'service_account.deleted', 'user.added', 'user.updated', 'user.deleted'.
    - `effective_at` (integer, required): The Unix timestamp (in seconds) of the event.
    - `project` (object, optional): The project that the action was scoped to. Absent for actions not scoped to projects. Note that any admin actions taken via Admin API keys are associated with the default project.
      - `id` (string, optional): The project ID.
      - `name` (string, optional): The project title.
    - `actor` (object, required): The actor who performed the audit logged action.
      - `type` (string, optional): The type of actor. Is either `session` or `api_key`. Enum: 'session', 'api_key'.
      - `session` (object, optional): The session in which the audit logged action was performed.
        - `user` (object, optional): The user who performed the audit logged action.
          - ...
        - `ip_address` (string, optional): The IP address from which the action was performed.
      - `api_key` (object, optional): The API Key used to perform the audit logged action.
        - `id` (string, optional): The tracking id of the API key.
        - `type` (string, optional): The type of API key. Can be either `user` or `service_account`. Enum: 'user', 'service_account'.
        - `user` (object, optional): The user who performed the audit logged action.
          - ...
        - `service_account` (object, optional): The service account that performed the audit logged action.
          - ...
    - `api_key.created` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The tracking ID of the API key.
      - `data` (object, optional): The payload used to create the API key.
        - `scopes` (array<string>, optional): A list of scopes allowed for the API key, e.g. `["api.model.request"]`
    - `api_key.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The tracking ID of the API key.
      - `changes_requested` (object, optional): The payload used to update the API key.
        - `scopes` (array<string>, optional): A list of scopes allowed for the API key, e.g. `["api.model.request"]`
    - `api_key.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The tracking ID of the API key.
    - `checkpoint.permission.created` (object, optional): The project and fine-tuned model checkpoint that the checkpoint permission was created for.
      - `id` (string, optional): The ID of the checkpoint permission.
      - `data` (object, optional): The payload used to create the checkpoint permission.
        - `project_id` (string, optional): The ID of the project that the checkpoint permission was created for.
        - `fine_tuned_model_checkpoint` (string, optional): The ID of the fine-tuned model checkpoint.
    - `checkpoint.permission.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the checkpoint permission.
    - `external_key.registered` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the external key configuration.
      - `data` (object, optional): The configuration for the external key.
    - `external_key.removed` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the external key configuration.
    - `group.created` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the group.
      - `data` (object, optional): Information about the created group.
        - `group_name` (string, optional): The group name.
    - `group.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the group.
      - `changes_requested` (object, optional): The payload used to update the group.
        - `group_name` (string, optional): The updated group name.
    - `group.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the group.
    - `scim.enabled` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the SCIM was enabled for.
    - `scim.disabled` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the SCIM was disabled for.
    - `invite.sent` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the invite.
      - `data` (object, optional): The payload used to create the invite.
        - `email` (string, optional): The email invited to the organization.
        - `role` (string, optional): The role the email was invited to be. Is either `owner` or `member`.
    - `invite.accepted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the invite.
    - `invite.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the invite.
    - `ip_allowlist.created` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the IP allowlist configuration.
      - `name` (string, optional): The name of the IP allowlist configuration.
      - `allowed_ips` (array<string>, optional): The IP addresses or CIDR ranges included in the configuration.
    - `ip_allowlist.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the IP allowlist configuration.
      - `allowed_ips` (array<string>, optional): The updated set of IP addresses or CIDR ranges in the configuration.
    - `ip_allowlist.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The ID of the IP allowlist configuration.
      - `name` (string, optional): The name of the IP allowlist configuration.
      - `allowed_ips` (array<string>, optional): The IP addresses or CIDR ranges that were in the configuration.
    - `ip_allowlist.config.activated` (object, optional): The details for events with this `type`.
      - `configs` (array<object>, optional): The configurations that were activated.
        - Items:
          - ...
    - `ip_allowlist.config.deactivated` (object, optional): The details for events with this `type`.
      - `configs` (array<object>, optional): The configurations that were deactivated.
        - Items:
          - ...
    - `login.succeeded` (object, optional): This event has no additional fields beyond the standard audit log attributes.
    - `login.failed` (object, optional): The details for events with this `type`.
      - `error_code` (string, optional): The error code of the failure.
      - `error_message` (string, optional): The error message of the failure.
    - `logout.succeeded` (object, optional): This event has no additional fields beyond the standard audit log attributes.
    - `logout.failed` (object, optional): The details for events with this `type`.
      - `error_code` (string, optional): The error code of the failure.
      - `error_message` (string, optional): The error message of the failure.
    - `organization.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The organization ID.
      - `changes_requested` (object, optional): The payload used to update the organization settings.
        - `title` (string, optional): The organization title.
        - `description` (string, optional): The organization description.
        - `name` (string, optional): The organization name.
        - `threads_ui_visibility` (string, optional): Visibility of the threads page which shows messages created with the Assistants API and Playground. One of `ANY_ROLE`, `OWNERS`, or `NONE`.
        - `usage_dashboard_visibility` (string, optional): Visibility of the usage dashboard which shows activity and costs for your organization. One of `ANY_ROLE` or `OWNERS`.
        - `api_call_logging` (string, optional): How your organization logs data from supported API calls. One of `disabled`, `enabled_per_call`, `enabled_for_all_projects`, or `enabled_for_selected_projects`
        - `api_call_logging_project_ids` (string, optional): The list of project ids if api_call_logging is set to `enabled_for_selected_projects`
    - `project.created` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The project ID.
      - `data` (object, optional): The payload used to create the project.
        - `name` (string, optional): The project name.
        - `title` (string, optional): The title of the project as seen on the dashboard.
    - `project.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The project ID.
      - `changes_requested` (object, optional): The payload used to update the project.
        - `title` (string, optional): The title of the project as seen on the dashboard.
    - `project.archived` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The project ID.
    - `project.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The project ID.
    - `rate_limit.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The rate limit ID
      - `changes_requested` (object, optional): The payload used to update the rate limits.
        - `max_requests_per_1_minute` (integer, optional): The maximum requests per minute.
        - `max_tokens_per_1_minute` (integer, optional): The maximum tokens per minute.
        - `max_images_per_1_minute` (integer, optional): The maximum images per minute. Only relevant for certain models.
        - `max_audio_megabytes_per_1_minute` (integer, optional): The maximum audio megabytes per minute. Only relevant for certain models.
        - `max_requests_per_1_day` (integer, optional): The maximum requests per day. Only relevant for certain models.
        - `batch_1_day_max_input_tokens` (integer, optional): The maximum batch input tokens per day. Only relevant for certain models.
    - `rate_limit.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The rate limit ID
    - `role.created` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The role ID.
      - `role_name` (string, optional): The name of the role.
      - `permissions` (array<string>, optional): The permissions granted by the role.
      - `resource_type` (string, optional): The type of resource the role belongs to.
      - `resource_id` (string, optional): The resource the role is scoped to.
    - `role.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The role ID.
      - `changes_requested` (object, optional): The payload used to update the role.
        - `role_name` (string, optional): The updated role name, when provided.
        - `resource_id` (string, optional): The resource the role is scoped to.
        - `resource_type` (string, optional): The type of resource the role belongs to.
        - `permissions_added` (array<string>, optional): The permissions added to the role.
        - `permissions_removed` (array<string>, optional): The permissions removed from the role.
        - `description` (string, optional): The updated role description, when provided.
        - `metadata` (object, optional): Additional metadata stored on the role.
    - `role.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The role ID.
    - `role.assignment.created` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The identifier of the role assignment.
      - `principal_id` (string, optional): The principal (user or group) that received the role.
      - `principal_type` (string, optional): The type of principal (user or group) that received the role.
      - `resource_id` (string, optional): The resource the role assignment is scoped to.
      - `resource_type` (string, optional): The type of resource the role assignment is scoped to.
    - `role.assignment.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The identifier of the role assignment.
      - `principal_id` (string, optional): The principal (user or group) that had the role removed.
      - `principal_type` (string, optional): The type of principal (user or group) that had the role removed.
      - `resource_id` (string, optional): The resource the role assignment was scoped to.
      - `resource_type` (string, optional): The type of resource the role assignment was scoped to.
    - `service_account.created` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The service account ID.
      - `data` (object, optional): The payload used to create the service account.
        - `role` (string, optional): The role of the service account. Is either `owner` or `member`.
    - `service_account.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The service account ID.
      - `changes_requested` (object, optional): The payload used to updated the service account.
        - `role` (string, optional): The role of the service account. Is either `owner` or `member`.
    - `service_account.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The service account ID.
    - `user.added` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The user ID.
      - `data` (object, optional): The payload used to add the user to the project.
        - `role` (string, optional): The role of the user. Is either `owner` or `member`.
    - `user.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The project ID.
      - `changes_requested` (object, optional): The payload used to update the user.
        - `role` (string, optional): The role of the user. Is either `owner` or `member`.
    - `user.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The user ID.
    - `certificate.created` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The certificate ID.
      - `name` (string, optional): The name of the certificate.
    - `certificate.updated` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The certificate ID.
      - `name` (string, optional): The name of the certificate.
    - `certificate.deleted` (object, optional): The details for events with this `type`.
      - `id` (string, optional): The certificate ID.
      - `name` (string, optional): The name of the certificate.
      - `certificate` (string, optional): The certificate content in PEM format.
    - `certificates.activated` (object, optional): The details for events with this `type`.
      - `certificates` (array<object>, optional)
        - Items:
          - ...
    - `certificates.deactivated` (object, optional): The details for events with this `type`.
      - `certificates` (array<object>, optional)
        - Items:
          - ...
- `first_id` (string, required)
- `last_id` (string, required)
- `has_more` (boolean, required)

## Returns
A list of paginated [Audit Log](object.md) objects.

## Examples
### Example
#### Request (curl)
```bash
curl https://api.openai.com/v1/organization/audit_logs \
-H "Authorization: Bearer $OPENAI_ADMIN_KEY" \
-H "Content-Type: application/json"
```
#### Response
```json
{
    "object": "list",
    "data": [
        {
            "id": "audit_log-xxx_yyyymmdd",
            "type": "project.archived",
            "effective_at": 1722461446,
            "actor": {
                "type": "api_key",
                "api_key": {
                    "type": "user",
                    "user": {
                        "id": "user-xxx",
                        "email": "user@example.com"
                    }
                }
            },
            "project.archived": {
                "id": "proj_abc"
            },
        },
        {
            "id": "audit_log-yyy__20240101",
            "type": "api_key.updated",
            "effective_at": 1720804190,
            "actor": {
                "type": "session",
                "session": {
                    "user": {
                        "id": "user-xxx",
                        "email": "user@example.com"
                    },
                    "ip_address": "127.0.0.1",
                    "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36",
                    "ja3": "a497151ce4338a12c4418c44d375173e",
                    "ja4": "q13d0313h3_55b375c5d22e_c7319ce65786",
                    "ip_address_details": {
                      "country": "US",
                      "city": "San Francisco",
                      "region": "California",
                      "region_code": "CA",
                      "asn": "1234",
                      "latitude": "37.77490",
                      "longitude": "-122.41940"
                    }
                }
            },
            "api_key.updated": {
                "id": "key_xxxx",
                "data": {
                    "scopes": ["resource_2.operation_2"]
                }
            },
        }
    ],
    "first_id": "audit_log-xxx__20240101",
    "last_id": "audit_log_yyy__20240101",
    "has_more": true
}
```
