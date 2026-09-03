---
description: >-
  在资产始终处于托管的情况下，将一种同质化资产兑换为另一种，并
  完成交易结算。
---

# 兑换

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
示例代码位于 [Github](../#demo-client)
{% endhint %}

## 交易汇率

<mark style="color:green;">`POST`</mark> `/v1/conversion/rate`

获取币种之间的兑换汇率。

#### 请求 Body

| 名称                                     | 类型   | 说明                                                                                                                                                                |
| ---------------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| symbol<mark style="color:red;">\*</mark> | String | 交易币对的符号，例如 btc-usdt                                                                                                                         |
| side<mark style="color:red;">\*</mark>   | String | <p>交易方向：buy 或 sell。<br><strong>buy</strong>：买入基准币种的价格。<br><strong>sell</strong>：卖出计价币种的价格。</p> |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
  "code": "200",
  "data": {
    "rate": "16078.8636472720095",
    "symbol": "ETH-USDT",
    "timeMills": 1678085017746,
    "expiredMills": 1678085077746
  },
  "message": "success"
}
```
{% endtab %}
{% endtabs %}

<details>

<summary>代码示例</summary>

```
curl --location --request POST 'https://api.musepay.io/v1/conversion/rate' \
--header 'Content-Type: application/json' \
--data-raw '{
   * "symbol": "BTC-USDT",
   * "side": "BUY"

}'
```

</details>

## 获取报价

<mark style="color:green;">`POST`</mark> `/v1/conversion/quote`

获取币种兑换报价。

#### 请求 Body

| 名称                                       | 类型   | 说明                                                                                                                                                                |
| ------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| symbol<mark style="color:red;">\*</mark>   | String | 交易币对的符号，例如 btc-usdt                                                                                                                         |
| amount<mark style="color:red;">\*</mark>   | String | 用于交易的资产金额                                                                                                                                              |
| currency<mark style="color:red;">\*</mark> | String | 用于交易的资产                                                                                                                                                    |
| side<mark style="color:red;">\*</mark>     | String | <p>交易方向：buy 或 sell。<br><strong>buy</strong>：买入基准币种的价格。<br><strong>sell</strong>：卖出计价币种的价格。</p> |
| xid<mark style="color:red;">\*</mark>      | String | 外部标识符，在该账户下创建的所有资源中唯一。                                                                                               |

{% tabs %}
{% tab title="200: OK " %}
{% code overflow="wrap" fullWidth="false" %}
```json
{
"code":"200",
"message":"success",
"data":
   {
      "quoteId":"2024102220000600011072223306",
      "payCurrency":"USDT",
      "payAmt":"100",
      "settleCurrency":"ETH",
      "settleAmt":"0.0375626384",
      "feeCurrency":"ETH",
      "feeAmt":"0.00003761",
      "rate":"2659.5569",
      "timeMills":1729581743749,
      "expiredMills":1729582343749
   }
}

```
{% endcode %}
{% endtab %}
{% endtabs %}

## 执行交易

<mark style="color:green;">`POST`</mark> `/v1/conversion/execute`

执行之前已报价的交易

#### 请求 Body

| 名称                                      | 类型   | 说明 |
| ----------------------------------------- | ------ | ----------- |
| quoteId<mark style="color:red;">\*</mark> | String | 报价 ID    |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
  "code": "200",
  "data": {
    "orderNo": "12323",
    "status": 22
  },
  "message": "success"
}
```
{% endtab %}
{% endtabs %}
