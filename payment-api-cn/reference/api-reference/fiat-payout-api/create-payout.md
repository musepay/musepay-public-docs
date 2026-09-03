# 创建法币出款

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md).
{% endhint %}

确认有效的出款报价并开始处理出款。

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/payouts/create`

## 请求 Body

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| order_no | String | 是 | [出款报价](quotations.md)接口返回的报价 `order_no`。 |
| purpose_code | String | 是 | 汇款用途代码。请保留前导零。 |
| description | String | 否 | 出款说明或参考信息。请勿包含敏感信息。 |

报价必须属于发起请求的 `partner_id`，不得过期，且必须仍处于初始状态。每个报价只能确认一次，重复确认将被拒绝。

## 请求示例

```json
{
  "order_no": "ORDER-1",
  "purpose_code": "02",
  "description": "monthly support"
}
```

## 响应 Body

| 名称 | 类型 | 说明 |
| --- | --- | --- |
| order_no | String | MusePay 生成的出款订单号。 |
| request_id | String | 创建报价时提供的标识符。 |
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
    "order_no": "ORDER-1",
    "request_id": "request-1",
    "pay_amount": "100.00",
    "pay_currency": "USDT",
    "receive_currency": "USD",
    "receive_amount": "98.75",
    "fee_amount": "1.25",
    "fee_currency": "USDT",
    "exchange_rate": "0.99",
    "status": 12,
    "failure_reason": null,
    "create_time": 1700000000000,
    "finish_time": null
  }
}
```
