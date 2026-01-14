# Costs object

Source: https://platform.openai.com/docs/api-reference/usage/costs_object

The aggregated costs details of the specific time bucket.

## Properties
- `object` (string, required) Enum: 'organization.costs.result'.
- `amount` (object, optional): The monetary value in its associated currency.
  - `value` (number, optional): The numeric value of the cost.
  - `currency` (string, optional): Lowercase ISO-4217 currency e.g. "usd"
- `line_item` (string | null, optional)
- `project_id` (string | null, optional)
