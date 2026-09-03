# 出款报价

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md).
{% endhint %}

创建将来源资产兑换为收款人所收法币的报价。创建报价时会记录收款人和出款通道。

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/payouts/quote`

## 请求 Body

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| request_id | String | 是 | 由组织提供的唯一标识符，用作报价请求的幂等键。 |
| quote_mode | String | 是 | 报价模式。使用 `source` 指定 `pay_amount`，或使用 `dest` 指定 `receive_amount`。 |
| pay_currency | String | 是 | 来源资产代码。 |
| pay_amount | String | 条件必填 | 来源金额。`quote_mode` 为 `source` 时必填，且必须大于零。 |
| receive_currency | String | 是 | 收款人收到的法币币种，使用 ISO 4217 币种代码。 |
| receive_amount | String | 条件必填 | 目标金额。`quote_mode` 为 `dest` 时必填，且必须大于零。 |
| beneficiary_country | String | 是 | 收款人所在国家或地区，使用 ISO 3166-1 alpha-2 代码。 |
| beneficiary_bank_id | String | 是 | [支持的银行](./capabilities/banks.md)返回的 `bank_code`。 |
| account_type | String | 是 | 收款人账户类型：个人使用 `PERSONAL`，组织使用 `ENTERPRISE`。 |
| beneficiary_relationship | String | 是 | 与收款人的关系：`own` 或 `third`。 |
| clear_network | String | 是 | [支持的清算网络](./capabilities/networks.md)返回的清算网络。 |
| beneficiaryFields | Object | 否 | 以[必需的收款人字段](./capabilities/fields.md)返回值为 key 的银行特定字段。字段名区分大小写。 |
| individual_beneficiary | Object | 条件必填 | `account_type` 为 `PERSONAL` 时必填。 |
| enterprise_beneficiary | Object | 条件必填 | `account_type` 为 `ENTERPRISE` 时必填。 |

仅提供与 `account_type` 匹配的收款人对象。

### 收款人字段

以下字段同时适用于 `individual_beneficiary` 和 `enterprise_beneficiary`：

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| account_no | String | 是 | 收款人银行账号。 |
| bank_name | String | 是 | 收款人银行名称。 |
| address | String | 是 | 收款人地址。 |

`individual_beneficiary` 的附加字段：

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| full_name | String | 否 | 法定全名。提供时，将用作收款人名称。 |
| first_name | String | 否 | 名。未提供 `full_name` 时，与 `middle_name` 和 `last_name` 搭配使用。 |
| middle_name | String | 否 | 中间名。 |
| last_name | String | 否 | 姓。 |
| nationality | String | 否 | 国籍，使用 ISO 3166-1 alpha-2 代码。 |
| gender | String | 否 | `male` 或 `female`。 |
| date_of_birth | String | 否 | 出生日期，格式为 `yyyy-MM-dd`。 |

`enterprise_beneficiary` 的附加字段：

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| company_name | String | 否 | 组织法定名称。 |

## 请求示例

```json
{
  "request_id": "request-1",
  "quote_mode": "source",
  "pay_currency": "USDT",
  "pay_amount": "100.00",
  "receive_currency": "USD",
  "beneficiary_country": "US",
  "beneficiary_bank_id": "bank-1",
  "account_type": "PERSONAL",
  "beneficiary_relationship": "third",
  "clear_network": "ACH",
  "beneficiaryFields": {
    "routing_number": "110000"
  },
  "individual_beneficiary": {
    "account_no": "123456789",
    "bank_name": "Example Bank",
    "address": "New York",
    "full_name": "Alice Smith"
  }
}
```

## 响应 Body

| 名称 | 类型 | 说明 |
| --- | --- | --- |
| request_id | String | 报价请求中提供的标识符。 |
| order_no | String | MusePay 生成的报价订单号。使用此值创建出款。 |
| transaction_time | Number | 报价创建时间，为 13 位 Unix 毫秒时间戳。 |
| quote_mode | String | 请求使用的报价模式。 |
| pay_amount | String | 从来源余额中扣除的金额。 |
| pay_currency | String | 来源资产代码。 |
| fee_amount | String | 出款费用。 |
| fee_currency | String | 费用的计价币种。 |
| exchange_rate | String | 从 `pay_currency` 到 `receive_currency` 的汇率。 |
| receive_amount | String | 收款人收到的法币金额。 |
| receive_currency | String | 收款人币种。 |
| expire_time | Number | 报价过期时间，为 13 位 Unix 毫秒时间戳。 |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "request_id": "request-1",
    "order_no": "ORDER-1",
    "transaction_time": 1700000000000,
    "quote_mode": "source",
    "pay_amount": "100.00",
    "pay_currency": "USDT",
    "fee_amount": "1.25",
    "fee_currency": "USDT",
    "exchange_rate": "0.99",
    "receive_amount": "98.75",
    "receive_currency": "USD",
    "expire_time": 1700000900000
  }
}
```
