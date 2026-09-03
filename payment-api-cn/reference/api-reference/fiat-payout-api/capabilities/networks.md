# 支持的清算网络

{% hint style="warning" %}
每个请求都必须包含[通用参数](../../common-parameters.md).
{% endhint %}

返回指定国家/地区和收款币种的清算网络。

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/networks`

## 请求 Body

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| country | String | 是 | 收款人所在国家或地区，使用 ISO 3166-1 alpha-2 代码。 |
| currency | String | 是 | 收款币种，使用 ISO 4217 币种代码。 |

```json
{
  "country": "US",
  "currency": "USD"
}
```

## 响应 Body

| 名称 | 类型 | 说明 |
| --- | --- | --- |
| networks | Array | 支持的清算网络代码。创建报价时选择其中一个作为 `clear_network`。 |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "networks": ["ACH"]
  }
}
```
