# 必需的收款人字段

{% hint style="warning" %}
每个请求都必须包含[通用参数](../../common-parameters.md).
{% endhint %}

返回指定国家/地区、币种和银行所需的银行特定收款人字段。创建报价时，请在 `beneficiaryFields` 中发送返回的 key。

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/fields`

## 请求 Body

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| country | String | 是 | 收款人所在国家或地区，使用 ISO 3166-1 alpha-2 代码。 |
| currency | String | 是 | 收款币种，使用 ISO 4217 币种代码。 |
| bank_code | String | 是 | 支持的银行接口返回的 MusePay 平台银行代码。 |
| network | String | 否 | 清算网络（可选）。对于银行类收款人，传入通过支持的网络接口选择的网络（例如 `LOCAL_PAYMENT`/`SWIFT`），以将返回字段限定为该网络。对于钱包类收款人或未选择网络时请省略，此时将返回完整字段集。 |

```json
{
  "country": "US",
  "currency": "USD",
  "bank_code": "bank-1",
  "network": "LOCAL_PAYMENT"
}
```

## 响应 Body

| 名称 | 类型 | 说明 |
| --- | --- | --- |
| fields | Array | 银行特定的收款人字段定义。 |
| fields[].key | String | 要在 `beneficiaryFields` 中发送的字段 key，区分大小写。 |
| fields[].label | String | 字段的显示名称。 |
| fields[].required | Boolean | 是否必须提供该字段。 |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "fields": [
      {
        "key": "routing_number",
        "label": "Routing number",
        "required": true
      }
    ]
  }
}
```
