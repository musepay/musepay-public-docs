# 支持的银行

{% hint style="warning" %}
每个请求都必须包含[通用参数](../../common-parameters.md).
{% endhint %}

返回某国家/地区和收款币种已启用的银行或钱包。提供 `amount` 时，结果会按通道限额过滤。

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/banks`

## 请求 Body

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| country | String | 是 | 收款人所在国家或地区，使用 ISO 3166-1 alpha-2 代码。 |
| currency | String | 是 | 收款币种，使用 ISO 4217 币种代码。 |
| amount | String | 否 | 用于根据通道支持的限额过滤银行的金额。 |

```json
{
  "country": "US",
  "currency": "USD",
  "amount": "100.00"
}
```

## 响应 Body

| 名称 | 类型 | 说明 |
| --- | --- | --- |
| banks | Array | 支持的银行或钱包条目。 |
| banks[].bank_code | String | MusePay 平台银行代码。创建报价时将其用作 `beneficiary_bank_id`。 |
| banks[].bank_name | String | 如有英文银行名称则返回英文名称，否则返回当地语言名称。 |
| banks[].type | String | 机构类型，例如 `bank` 或 `wallet`。 |
| banks[].clearing_networks | Array | 该国家/地区和币种可用的清算网络。 |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "banks": [
      {
        "bank_code": "bank-1",
        "bank_name": "Example Bank",
        "type": "bank",
        "clearing_networks": ["ACH"]
      }
    ]
  }
}
```
