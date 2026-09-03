# 查询法币出款

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md).
{% endhint %}

获取出款订单及其最新状态。

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/payouts/query`

## 请求 Body

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| request_id | String | 条件必填 | 由组织提供的出款标识符。`request_id` 和 `order_no` 二选一。 |
| order_no | String | 条件必填 | MusePay 生成的出款订单号。`order_no` 和 `request_id` 二选一。 |

## 请求示例

```json
{
  "request_id": "ORD-20260505-001"
}
```

## 响应 Body

| 名称 | 类型 | 说明 |
| --- | --- | --- |
| order_no | String | MusePay 生成的出款订单号。 |
| request_id | String | 由组织提供的出款标识符。 |
| pay_amount | String | 从来源余额中扣除的金额。 |
| pay_currency | String | 来源资产代码。 |
| receive_currency | String | 收款人收到的法币币种。 |
| receive_amount | String | 收款人收到的法币金额。 |
| fee_amount | String | 出款费用。 |
| fee_currency | String | 费用的计价币种。 |
| exchange_rate | String | 出款使用的汇率。 |
| status | Number | 当前[订单状态](../../../enums/order-status.md). |
| failure_reason | String | 失败原因（如有）。 |
| create_time | Number | 订单创建时间，为 13 位 Unix 毫秒时间戳。 |
| finish_time | Number | 订单完成时间，为 13 位 Unix 毫秒时间戳；如有则返回。 |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "order_no": "PO202605050001",
    "request_id": "ORD-20260505-001",
    "pay_amount": "1000.00",
    "pay_currency": "USDT",
    "receive_currency": "USD",
    "receive_amount": "995.00",
    "fee_amount": "5.00",
    "fee_currency": "USDT",
    "exchange_rate": "1.0000",
    "status": 99,
    "failure_reason": null,
    "create_time": 1777946400000,
    "finish_time": 1777946700000
  }
}
```

## 出款状态通知

每当出款状态变更时，MusePay 都会发送订单 Webhook。通知使用标准[订单 Webhook](../../../webhook/order.md) Payload 和现有的[订单状态](../../../enums/order-status.md)值。

处理通知时，请使用 `order_no` 或 `request_id` 作为幂等键，并在通知成功处理后返回 HTTP `200`。
