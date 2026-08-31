# Rate



{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](../#demo-client)
{% endhint %}

## Trade Rate

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/rate/queryTradeRate`

Retrieves exchange rate between currencies.

#### Request Body

| Name                                            | Type   | Description                                                        |
| ----------------------------------------------- | ------ | ------------------------------------------------------------------ |
| baseCurrency<mark style="color:red;">\*</mark>  | String | the first currency appearing in a currency pair                    |
| quoteCurrency<mark style="color:red;">\*</mark> | String | used to determine the value of the base currency                   |
| symbolTradeType                                 | String | buy or sell base on baseCurrency,default sell,                     |
| orderType                                       | String | used for specific business types and can be left empty by default. |

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
