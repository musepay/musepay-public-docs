---
description: Choose between multi-chain and specified-chain Checkout Mode payments.
---

# Checkout Payment Methods

Checkout Mode supports two payment experiences controlled by `payment_method`. Choose whether the user can select a supported USDT network on the checkout page or whether your order requires a specific network.

## At a glance

| Checkout experience | `payment_method` | `currency` or `pay_currency` | User experience |
| --- | --- | --- | --- |
| Multi-chain checkout | `on_line` | `USDT` | The checkout page lets the user choose any supported network for USDT. |
| Specified-chain checkout | `on_chain` | A chain-specific asset such as `USDT_TRC20` | The checkout page and returned payment address are fixed to the specified network. |

## Which currency field to use

The field depends on how the order amount is denominated:

* For a crypto-denominated order, set `currency` to `USDT` or a chain-specific USDT asset.
* For a fiat-denominated order, set `currency` to the fiat currency and use `pay_currency` to control how the user pays.

## Multi-chain checkout with `on_line`

Use `payment_method=on_line` when you want the user to choose the payment network on the hosted checkout page. Set the applicable payment asset field to the generic `USDT` code.

For a crypto-denominated order, the relevant fields are:

```json
{
  "payment_method": "on_line",
  "currency": "USDT"
}
```

For a fiat-denominated order, keep the fiat currency in `currency` and set `pay_currency` to `USDT`:

```json
{
  "payment_method": "on_line",
  "currency": "IDR",
  "pay_currency": "USDT"
}
```

The user can then choose any USDT network supported by MusePay.

<figure><img src="../../.gitbook/assets/checkout-on-line.png" alt="Hosted checkout generated with payment_method set to on_line"><figcaption>The <code>on_line</code> checkout lets the user select a supported USDT network before paying.</figcaption></figure>

{% content-ref url="../../reference/api-reference/acquiring-api/checkout-mode/multiple-chain-checkout.md" %}
[Multiple Chain Checkout example](../../reference/api-reference/acquiring-api/checkout-mode/multiple-chain-checkout.md)
{% endcontent-ref %}

## Specified-chain checkout with `on_chain`

Use `payment_method=on_chain` when the order must be paid on a specific network. Set the applicable payment asset field to a chain-specific code such as `USDT_TRC20`.

For a crypto-denominated order, the relevant fields are:

```json
{
  "payment_method": "on_chain",
  "currency": "USDT_TRC20"
}
```

For a fiat-denominated order, keep the fiat currency in `currency` and specify the network in `pay_currency`:

```json
{
  "payment_method": "on_chain",
  "currency": "IDR",
  "pay_currency": "USDT_TRC20"
}
```

The hosted checkout page and the address returned for the order will accept USDT on that network only.

{% content-ref url="../../reference/api-reference/acquiring-api/checkout-mode/specified-chain-checkout.md" %}
[Specified Chain Checkout example](../../reference/api-reference/acquiring-api/checkout-mode/specified-chain-checkout.md)
{% endcontent-ref %}

{% hint style="warning" %}
Use the generic `USDT` code only with `on_line`. With `on_chain`, select a chain-specific USDT code from [Supported Assets](../supported-assets.md). Sending funds over a different network may result in the payment not being credited.
{% endhint %}

## Related references

* [Create Checkout Order](../../reference/api-reference/acquiring-api/checkout-mode/README.md)
* [Checkout Payment Amount Handling](checkout-payment-amount-handling.md)
* [Order webhook](../../webhook/order.md)
