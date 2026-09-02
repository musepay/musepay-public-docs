---
description: Integrate fiat payouts from a USDT balance to third-party bank accounts.
---

# Fiat Payout API

The Fiat Payout API lets your organization send fiat currency from its USDT balance to a third-party bank account. A payout is created through a quote-first workflow and processed asynchronously.

{% hint style="info" %}
A successful API response confirms that the request was accepted, not that the payout has completed. Use the query endpoint or an [order webhook](../../webhook/order.md) to obtain the final result.
{% endhint %}

## Before you begin

* Complete [Authentication](../authentication.md) and include the required [common parameters](../../reference/api-reference/common-parameters.md) in every request.
* Fund your partner basic account with sufficient USDT for the payout and applicable fees.
* Implement [order webhooks](../../webhook/order.md) or plan to poll the query endpoint for asynchronous status updates.

## Integration flow

### 1. Discover payout capabilities

Use the [capabilities](../../reference/api-reference/fiat-payout-api/capabilities/README.md) endpoints to select a supported country, currency, bank or wallet, and clearing network. Retrieve the required beneficiary fields for the selected route instead of hard-coding them.

### 2. Create a payout quote

[Create a payout quote](../../reference/api-reference/fiat-payout-api/quotations.md) with the selected route, amount, remittance purpose, and beneficiary details. Store the returned `order_no` and note the quote expiry time.

### 3. Create the payout

[Create the payout](../../reference/api-reference/fiat-payout-api/create-payout.md) with the valid, unexpired quote `order_no`. Each quote can be confirmed only once.

### 4. Track the final status

[Query the payout](../../reference/api-reference/fiat-payout-api/query-payout.md) or process order webhooks until the payout reaches a final [order status](../../enums/order-status.md). Do not treat the create response as proof of completion.

## Key rules

| Rule | Description |
| --- | --- |
| Capability discovery | Query the support endpoints before quoting because available routes and required fields can vary by country, currency, bank, and amount. |
| Quote idempotency | Use a unique `request_id` for each quote request. Its scope includes the common `partner_id`. |
| Quote required | Create the payout with the valid, unexpired `order_no` returned by the quote endpoint. Each quote can be confirmed only once. |
| Beneficiary type | Use `individual_beneficiary` for `account_type=01` or `enterprise_beneficiary` for `account_type=03`. |
| Dynamic fields | Send fields returned by `/supports/fields` in the case-sensitive `beneficiaryFields` object when creating a quote. |
| Remittance purpose | Use a supported `purpose_code` and preserve leading zeroes. |
| Asynchronous status | Creating a payout does not mean it has completed. Use the query API or order webhooks to obtain its final status. |

## Endpoint reference

For request parameters, response schemas, and endpoint details, see the [Fiat Payout API Reference](../../reference/api-reference/fiat-payout-api/README.md).
