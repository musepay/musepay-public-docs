---
description: 处理 Checkout Mode 中金额完全一致、少付和多付的付款。
---

# 收银台付款金额处理

在 Checkout Mode 中，用户发送的金额可能与订单要求的金额不同。在决定为用户入账多少价值前，您的集成必须区分预期订单金额和用户实际支付金额。

## 默认行为

默认情况下，只有当用户的支付金额与订单金额完全一致时，Checkout Mode 订单才会成功，MusePay 才会发送支付成功通知：

```
pay_amount = order_amount
```

## 允许少付和多付

我们建议在用户少付或多付时也允许订单成功。启用少付和多付后，MusePay 会按实际收到的金额处理，通过[订单 Webhook](../../webhook/order.md)发送该金额，并将计算后的净额计入您的商户余额。

{% hint style="info" %}
如需启用少付和多付，请联系 MusePay 运营团队为您的账户配置此选项。
{% endhint %}

Webhook 中金额字段的含义如下：

| 字段 | 含义 |
| --- | --- |
| `order_amount` | 创建 Checkout Mode 订单时请求的金额。 |
| `pay_amount` | 用户实际支付的金额。 |
| `fee_amount` | 根据 `pay_amount` 计算的服务费。 |
| `actual_amount` | 扣除手续费后计入商户余额的净额。 |

计算方式如下：

```
fee_amount = pay_amount × fee rate
actual_amount = pay_amount - fee_amount
```

MusePay 根据实际支付金额计算手续费，而不是根据原始订单金额。该规则同时适用于少付和多付。

## 示例：少付

假设订单金额为 `100 USDT`，用户支付 `99 USDT`，手续费率为 `1%`。

| 字段 | 值 | 计算 |
| --- | --- | --- |
| `order_amount` | `100 USDT` | 原始订单金额 |
| `pay_amount` | `99 USDT` | 实际收到的金额 |
| `fee_amount` | `0.99 USDT` | `99 × 1%` |
| `actual_amount` | `98.01 USDT` | `99 - 0.99` |

Webhook 会通知这些数值，MusePay 将 `98.01 USDT` 计入您的商户余额。

## 选择用户入账策略

MusePay 会根据实际收到的付款为商户余额入账。您的系统仍需自行决定是否以及如何为终端用户入账。

常见的处理方式如下：

{% hint style="info" %}
每个收银台流程请在以下互斥策略中选择一种。这些策略是备选方案，不应叠加使用。
{% endhint %}

### 选项 1：要求金额完全一致

仅当两个金额相同时为用户入账：

```
pay_amount = order_amount
```

### 选项 2：允许配置的差额范围

仅当绝对差额在业务配置的限制范围内时为用户入账：

```
abs(pay_amount - order_amount) <= configured tolerance
```

### 选项 3：按实际支付金额入账

无论原始 `order_amount` 是多少，均按 `pay_amount` 为用户入账。

{% hint style="warning" %}
比较或计算货币金额时请使用十进制精确算术，并保证 Webhook 处理幂等，防止同一笔付款重复为用户入账。
{% endhint %}

## 相关参考

* [收单 API 集成指南](README.md)
* [创建收银台订单](../../reference/api-reference/acquiring-api/checkout-mode/README.md)
* [订单 Webhook 字段](../../webhook/order.md)
* [查询订单](../../reference/api-reference/acquiring-api/query-order.md)
