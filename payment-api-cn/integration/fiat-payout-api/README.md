---
description: 集成从 USDT 余额到第三方银行账户的法币出款。
---

# 法币出款 API

Fiat Payout API 允许您的组织使用 USDT 余额向第三方银行账户发送法币。出款需要先创建报价，并以异步方式处理。

{% hint style="info" %}
API 返回成功仅表示请求已被接受，不代表出款已完成。请使用查询接口或[订单 Webhook](../../webhook/order.md)获取最终结果。
{% endhint %}

## 开始之前

* 完成[身份验证](../authentication.md)，并在每个请求中包含所需的[通用参数](../../reference/api-reference/common-parameters.md)。
* 确保 partner basic account 中有足够的 USDT 以支付出款金额和相关费用。
* 实现[订单 Webhook](../../webhook/order.md)，或计划轮询查询接口以获取异步状态更新。

## 集成流程

### 1. 查询出款能力

使用[出款能力](../../reference/api-reference/fiat-payout-api/capabilities/README.md)接口选择支持的国家、币种、银行或钱包以及清算网络。请动态获取所选通道需要的收款人字段，不要在代码中写死。

### 2. 创建出款报价

使用所选通道、金额、汇款用途和收款人详情[创建出款报价](../../reference/api-reference/fiat-payout-api/quotations.md)。保存返回的 `order_no`，并注意报价过期时间。

### 3. 创建出款

使用有效且未过期的报价 `order_no` [创建出款](../../reference/api-reference/fiat-payout-api/create-payout.md)。每个报价只能确认一次。

### 4. 跟踪最终状态

[查询出款](../../reference/api-reference/fiat-payout-api/query-payout.md)或处理订单 Webhook，直到出款达到最终[订单状态](../../enums/order-status.md)。请勿将创建响应视为出款已完成的证明。

## 重要规则

| Rule | 说明 |
| --- | --- |
| 能力查询 | 报价前请查询支持能力接口，因为可用通道和必填字段可能因国家、币种、银行和金额而异。 |
| 报价幂等性 | 每个报价请求请使用唯一的 `request_id`，其唯一性范围包含通用参数 `partner_id`。 |
| 必须先报价 | 使用报价接口返回的有效且未过期 `order_no` 创建出款。每个报价只能确认一次。 |
| 收款人类型 | `account_type=01` 时使用 `individual_beneficiary`；`account_type=03` 时使用 `enterprise_beneficiary`。 |
| 动态字段 | 创建报价时，在区分大小写的 `beneficiaryFields` 对象中发送 `/supports/fields` 返回的字段。 |
| 汇款用途 | 使用受支持的 `purpose_code`，并保留前导零。 |
| 异步状态 | 创建出款不代表出款已完成。请使用查询 API 或订单 Webhook 获取最终状态。 |

## 接口参考

有关请求参数、响应数据结构和接口详情，请参见 [Fiat Payout API 参考](../../reference/api-reference/fiat-payout-api/README.md)。
