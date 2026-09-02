# Fiat Payout API

Use these endpoints to discover supported payout routes, create a quote, submit a fiat payout from a USDT balance, and retrieve its status.

{% hint style="info" %}
For the recommended implementation sequence and operational requirements, see the [Fiat Payout API integration guide](../../../integration/fiat-payout-api/README.md).
{% endhint %}

<<<<<<< HEAD
=======
## Integration Flow

1. Use the [capabilities](./capabilities/README.md) endpoints to select a country, currency, bank, clearing network, and required beneficiary fields.
2. [Create a payout quote](quotations.md) with the selected route and beneficiary details.
3. [Create the payout](create-payout.md) with the quote `order_no` before the quote expires.
4. [Query the payout](query-payout.md) or process order webhooks until it reaches a final [order status](../../../enums/order-status.md).

## Key Rules

| Rule | Description |
| --- | --- |
| Capability discovery | Query the support endpoints before quoting because available routes and required fields can vary by country, currency, bank, and amount. |
| Quote idempotency | Use a unique `request_id` for each quote request. Its scope includes the common `partner_id`. |
| Quote required | Create the payout with the valid, unexpired `order_no` returned by the quote endpoint. Each quote can be confirmed only once. |
| Beneficiary type | Use `individual_beneficiary` for `account_type=PERSONAL` or `enterprise_beneficiary` for `account_type=ENTERPRISE`. |
| Dynamic fields | Send fields returned by `/supports/fields` in the case-sensitive `beneficiaryFields` object when creating a quote. |
| Remittance purpose | Use a supported `purpose_code` and preserve leading zeroes. |
| Asynchronous status | Creating a payout does not mean it has completed. Use the query API or order webhooks to obtain its final status. |

>>>>>>> main
## APIs

| API | Endpoint | Description |
| --- | --- | --- |
| [Payout Quote](quotations.md) | `/v1/fiatpayout/payouts/quote` | Create a payout quote and capture beneficiary details. |
| [Create Fiat Payout](create-payout.md) | `/v1/fiatpayout/payouts/create` | Confirm a valid quote and start payout processing. |
| [Query Fiat Payout](query-payout.md) | `/v1/fiatpayout/payouts/query` | Retrieve a payout and its latest status. |
| [Remittance Purposes](remittance-purposes.md) | `/v1/fiatpayout/payouts/remitReasons` | Retrieve available remittance purpose codes. |
| [Supported Countries](./capabilities/countries.md) | `/v1/fiatpayout/supports/countries` | Retrieve supported countries and currencies. |
| [Supported Banks](./capabilities/banks.md) | `/v1/fiatpayout/supports/banks` | Retrieve banks or wallets supported for a route. |
| [Supported Networks](./capabilities/networks.md) | `/v1/fiatpayout/supports/networks` | Retrieve clearing networks supported for a route. |
| [Required Beneficiary Fields](./capabilities/fields.md) | `/v1/fiatpayout/supports/fields` | Retrieve bank-specific beneficiary fields. |
