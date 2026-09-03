# 支持的国家/地区

{% hint style="warning" %}
每个请求都必须包含[通用参数](../../common-parameters.md).
{% endhint %}

返回支持的收款人国家/地区，以及每个国家/地区可用的法币币种。

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/countries`

## 请求 Body

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| receive_currency | String | 否 | 将结果限制为指定收款币种。省略此参数时，返回所有支持的国家/地区和币种组合。 |

```json
{
  "receive_currency": "USD"
}
```

## 响应 Body

| 名称 | 类型 | 说明 |
| --- | --- | --- |
| countries | Array | 支持的国家/地区条目，按国家代码排序。 |
| countries[].country | String | 国家或地区，使用 ISO 3166-1 alpha-2 代码。 |
| countries[].currencies | Array | 该国家/地区支持的收款币种。 |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "countries": [
      {
        "country": "US",
        "currencies": ["USD"]
      }
    ]
  }
}
```
