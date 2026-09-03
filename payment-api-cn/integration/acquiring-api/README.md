---
description: 选择并集成适合您支付流程的 MusePay 数字货币收单模式。
---

# 收单 API

MusePay 支持两种数字货币收单模式。当每位用户需要一个可重复使用的充值地址时，请选择 **Wallet Mode（用户专属地址）**；当系统需要在每次付款前创建支付订单时，请选择 **Checkout Mode（按订单分配地址）**。

两种模式都会在检测到充值后通知您的系统。主要区别在于本地订单的创建时机，以及收款地址与支付场景保持关联的时间。

## 选择集成模式

| | Wallet Mode（用户专属地址） | Checkout Mode（按订单分配地址） |
| --- | --- | --- |
| 地址分配 | 每位用户一个固定地址 | 每笔订单一个临时地址 |
| 地址有效期 | 可供后续充值重复使用 | 默认有效期为一天 |
| 本地订单创建时机 | 收到充值通知后创建 | 请求支付地址前创建 |
| 金额处理 | 按 MusePay 通知的实际金额入账 | 将充值金额与订单金额核对 |
| 适用场景 | 钱包充值、储值余额和重复使用的用户 | 电商收银台和一次性付款 |

## Wallet Mode（用户专属地址）

Wallet Mode 会为每位用户分配一个固定充值地址。用户可以随时向该地址充值。MusePay 检测并确认充值后，会向您的系统发送包含到账金额的订单 Webhook。您的系统随后创建本地订单，并为用户余额入账。

<figure><img src="../../.gitbook/assets/acquiring-wallet-mode.png" alt="用户专属地址流程"><figcaption>每位用户对应一个可重复使用的充值地址。</figcaption></figure>

### 集成流程

1. 完成[身份验证](../authentication.md)并实现[订单 Webhook](../../webhook/order.md)。
2. 调用[充值地址](../../reference/api-reference/acquiring-api/wallet-mode.md#deposit-address)接口，传入资产和您的 `customer_ref_id`，以获取用户地址。
3. 保存用户、资产与返回地址之间的关联关系。
4. 允许用户在需要时随时向该地址充值。
5. 收到 Webhook 后验证签名，并使用通知中的金额和 `customerRefId` 创建本地订单，为正确的用户入账。
6. 需要获取交易详情时，请使用[查询](../../reference/api-reference/acquiring-api/wallet-mode.md#query)接口。

{% hint style="warning" %}
Webhook 处理必须保证幂等，同一事件不得重复为用户余额入账。
{% endhint %}

## Checkout Mode（按订单分配地址）

Checkout Mode 会为每笔订单创建新的支付场景。您的系统先创建订单，MusePay 随后返回一个默认有效期为一天的临时收款地址。用户充值后，MusePay 会发送订单 Webhook。

<figure><img src="../../.gitbook/assets/acquiring-order-mode.png" alt="按订单分配地址流程"><figcaption>每笔订单都会获得独立的临时支付地址。</figcaption></figure>

### 集成流程

1. 完成[身份验证](../authentication.md)并实现[订单 Webhook](../../webhook/order.md)。
2. 在您的系统中使用唯一请求 ID 和预期金额创建本地订单。
3. 调用[创建收银台订单](../../reference/api-reference/acquiring-api/checkout-mode/README.md#create-checkout-order)，获取订单号、收款地址和收银台 URL。
4. 在地址过期前向用户展示地址或收银台 URL。
5. 收到 Webhook 后验证签名，并在履约前将通知的付款信息与本地订单核对。
6. 需要时使用[查询订单](../../reference/api-reference/acquiring-api/query-order.md)获取最新订单状态。

{% content-ref url="checkout-payment-methods.md" %}
[收银台支付方式](checkout-payment-methods.md)
{% endcontent-ref %}

{% hint style="info" %}
付款可能少付、多付，或在地址过期后到账。定义履约规则前，请阅读[收银台付款金额处理](checkout-payment-amount-handling.md)，并以 Webhook 或查询结果作为履约依据，而不是初始创建订单响应。
{% endhint %}

{% content-ref url="checkout-payment-amount-handling.md" %}
[收银台付款金额处理](checkout-payment-amount-handling.md)
{% endcontent-ref %}

## 相关参考

* [支持的资产](../supported-assets.md)
* [Wallet Mode 接口](../../reference/api-reference/acquiring-api/wallet-mode.md)
* [Checkout Mode 接口](../../reference/api-reference/acquiring-api/checkout-mode/README.md)
* [收银台支付方式](checkout-payment-methods.md)
* [收银台付款金额处理](checkout-payment-amount-handling.md)
* [订单 Webhook](../../webhook/order.md)
* [订单状态](../../enums/order-status.md)
