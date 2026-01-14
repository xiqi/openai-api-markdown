# The group user object

Source: https://platform.openai.com/docs/api-reference/groups/users/assignment-object

Confirmation payload returned after adding a user to a group.

## Properties
- `object` (string, required): Always `group.user`. Enum: 'group.user'.
- `user_id` (string, required): Identifier of the user that was added.
- `group_id` (string, required): Identifier of the group the user was added to.
