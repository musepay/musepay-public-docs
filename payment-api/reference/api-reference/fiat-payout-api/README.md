# Fiat Payout API

Use these endpoints to discover supported payout routes, create a quote, submit a fiat payout from a USDT balance, and retrieve its status.

{% hint style="info" %}
For the recommended implementation sequence and operational requirements, see the [Fiat Payout API integration guide](../../../integration/fiat-payout-api/README.md).
{% endhint %}

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
