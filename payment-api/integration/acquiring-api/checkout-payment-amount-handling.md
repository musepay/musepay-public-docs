---
description: Handle exact, underpaid, and overpaid Checkout Mode payments.
---

# Checkout Payment Amount Handling

In Checkout Mode, the amount a user sends may differ from the amount requested by the order. Your integration must distinguish the expected order amount from the amount actually paid before deciding how much value to credit to the user.

## Default behavior

By default, a Checkout Mode order succeeds and MusePay sends the successful payment notification only when the user's payment amount exactly matches the order amount:

```
pay_amount = order_amount
```

## Allowing underpayments and overpayments

We recommend allowing orders to succeed when a user pays less or more than the order amount. When underpayments and overpayments are accepted, MusePay processes the amount actually received, sends it in the [order webhook](../../webhook/order.md), and credits the resulting net amount to your merchant balance.

{% hint style="info" %}
To enable underpayments and overpayments, contact the MusePay Operations Team to configure this option for your account.
{% endhint %}

The webhook amount fields have the following meanings:

| Field | Meaning |
| --- | --- |
| `order_amount` | The amount requested when the Checkout Mode order was created. |
| `pay_amount` | The amount actually paid by the user. |
| `fee_amount` | The service fee calculated from `pay_amount`. |
| `actual_amount` | The net amount credited to your merchant balance after the fee is deducted. |

The calculation is:

```
fee_amount = pay_amount × fee rate
actual_amount = pay_amount - fee_amount
```

MusePay calculates the fee from the amount actually paid, not from the original order amount. This applies to both underpayments and overpayments.

## Example: underpayment

Assume the order amount is `100 USDT`, the user pays `99 USDT`, and the fee rate is `1%`.

| Field | Value | Calculation |
| --- | --- | --- |
| `order_amount` | `100 USDT` | Original order amount |
| `pay_amount` | `99 USDT` | Amount actually received |
| `fee_amount` | `0.99 USDT` | `99 × 1%` |
| `actual_amount` | `98.01 USDT` | `99 - 0.99` |

The webhook reports these values, and MusePay credits `98.01 USDT` to your merchant balance.

## Choose your user-crediting policy

MusePay credits the merchant balance based on the payment received. Your system remains responsible for deciding whether and how to credit the end user.

Common approaches include:

{% hint style="info" %}
Choose one of the following mutually exclusive policies for each Checkout flow. These policies are alternatives and should not be applied cumulatively.
{% endhint %}

### Option 1: Require an exact payment

Credit the user only when the two amounts match:

```
pay_amount = order_amount
```

### Option 2: Allow a configured tolerance

Credit the user only when the absolute difference is within a limit defined by your business:

```
abs(pay_amount - order_amount) <= configured tolerance
```

### Option 3: Credit the amount actually paid

Credit the user according to `pay_amount`, regardless of the original `order_amount`.

{% hint style="warning" %}
Use decimal arithmetic when comparing or calculating currency amounts, and process webhooks idempotently so the same payment cannot credit a user more than once.
{% endhint %}

## Related references

* [Acquiring API integration guide](README.md)
* [Create Checkout Order](../../reference/api-reference/acquiring-api/checkout-mode/README.md)
* [Order webhook fields](../../webhook/order.md)
* [Query Order](../../reference/api-reference/acquiring-api/query-order.md)
