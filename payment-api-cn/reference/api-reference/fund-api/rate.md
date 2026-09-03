# 汇率



{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
示例代码位于 [Github](../#demo-client)
{% endhint %}

## 交易汇率

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/rate/queryTradeRate`

获取币种之间的兑换汇率。

#### 请求 Body

| 名称                                            | 类型   | 说明                                                        |
| ----------------------------------------------- | ------ | ------------------------------------------------------------------ |
| baseCurrency<mark style="color:red;">\*</mark>  | String | 币对中的第一个币种                    |
| quoteCurrency<mark style="color:red;">\*</mark> | String | 用于确定基准币种的价值                   |
| symbolTradeType                                 | String | 根据 baseCurrency 买入或卖出，默认为 sell                     |
| orderType                                       | String | 用于指定业务类型，默认可留空。 |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
  "code": "200",
  "data": {
    "rate": "16078.8636472720095",
    "symbol": "USDT-IDR",
    "timeMills": 1678085017746,
    "expiredMills": 1678085077746
  },
  "message": "success"
}
```
{% endtab %}
{% endtabs %}
