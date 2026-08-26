# Fiat Payout API

The Fiat Payout API lets an organization send fiat currency from its USDT balance to a third-party bank account.

{% hint style="info" %}
A successful API response confirms that the request was accepted. Fiat payouts are processed asynchronously. Use the query endpoint or an [order webhook](../../../webhook/order.md) to obtain the final result.
{% endhint %}

## Integration Flow

1. [Create a payout quote](quotations.md) for the destination country and fiat currency.
2. [Create the payout](create-payout.md) with a valid `customer_quote_no` before the quote expires.
3. [Upload supporting documents](upload-attachment.md) if they are required for the payout.
4. [Query the payout](query-payout.md) or process order webhooks until it reaches a final [order status](../../../enums/order-status.md).

## Key Rules

| Rule                | Description                                                                                                            |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Quote required      | Every payout must be created from a valid, unexpired quote.                                                            |
| Idempotency         | Use a unique `customer_quote_no` and `request_id` for each business request.                                            |
| Beneficiary type    | A local payout uses `beneficiary`; an international wire uses either `individual_beneficiary` or `enterprise_beneficiary`, matching the quote. |
| Remittance purpose  | Use a supported `remittance_purpose_code` and preserve leading zeroes.                                                  |
| Asynchronous status | Creating a payout does not mean it has completed. Use the query API or order webhooks to obtain its final status.      |

## APIs

| API                                              | Endpoint                              | Description                                            |
| ------------------------------------------------ | ------------------------------------- | ------------------------------------------------------ |
| [Payout Quotations](quotations.md)               | `/v1/fiatpayout/quotations/create`    | Create a local payout or international wire quote.     |
| [Payout Quotations](quotations.md)               | `/v1/fiatpayout/quotations/query`     | Query a quote by its MusePay or customer quote number. |
| [Create Fiat Payout](create-payout.md)           | `/v1/fiatpayout/payouts/create`       | Create a payout from a valid quote.                    |
| [Upload Payout Attachment](upload-attachment.md) | `/v1/fiatpayout/payouts/files/upload` | Upload a supporting document for a payout.             |
| [Query Fiat Payout](query-payout.md)             | `/v1/fiatpayout/payouts/query`        | Retrieve a payout and its latest status.               |
| [Remittance Purposes](remittance-purposes.md)    | `/v1/fiatpayout/payouts/remitReasons` | Retrieve available remittance purpose codes.           |
