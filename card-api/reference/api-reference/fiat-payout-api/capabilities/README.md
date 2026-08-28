# Capabilities

Use these endpoints before creating a payout quote. Available banks, clearing networks, and beneficiary fields can vary by country and currency. The optional bank-query amount can also affect which banks are available.

| API | Endpoint | Description |
| --- | --- | --- |
| [Supported Countries](countries.md) | `/v1/fiatpayout/supports/countries` | Retrieve supported countries and currencies. |
| [Supported Banks](banks.md) | `/v1/fiatpayout/supports/banks` | Retrieve banks or wallets supported for a route. |
| [Supported Networks](networks.md) | `/v1/fiatpayout/supports/networks` | Retrieve clearing networks supported for a route. |
| [Required Beneficiary Fields](fields.md) | `/v1/fiatpayout/supports/fields` | Retrieve bank-specific beneficiary fields. |
