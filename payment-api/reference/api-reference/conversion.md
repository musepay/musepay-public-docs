---
description: >-
  Convert from one fungible asset to another and settle transactions without
  ever taking assets out of custody.
---

# Conversion

{% hint style="warning" %}
Every request must contain [common parameters](common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](./#demo-client)
{% endhint %}

## Trade Rate

<mark style="color:green;">`POST`</mark> `/v1/conversion/rate`

Retrieves exchange rate between currencies.

#### Request Body

| Name                                     | Type   | Description                                                                                                                                                                |
| ---------------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| symbol<mark style="color:red;">\*</mark> | String | Symbol of the pair to trade, for example, btc-usdt                                                                                                                         |
| side<mark style="color:red;">\*</mark>   | String | <p>side of trade: buy or sell.<br><strong>buy</strong>:  the price for buying the base currency.<br><strong>sell</strong>:   the price for selling the quote currency.</p> |

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

<summary>Code Example</summary>

```
curl --location --request POST 'https:///api.musepay.io/v1/rate/queryTradeRate' \
--header 'Content-Type: application/json' \
--data-raw '{
   * "symbol": "BTC-USDT",
   * "side": "BUY"
   
}'
```

</details>

## Get a Quote

<mark style="color:green;">`POST`</mark> `/v1/conversion/quote`

Get a quote for currency conversion.

#### Request Body

| Name                                       | Type   | Description                                                                                                                                                                |
| ------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| symbol<mark style="color:red;">\*</mark>   | String | Symbol of the pair to trade, for example, btc-usdt                                                                                                                         |
| amount<mark style="color:red;">\*</mark>   | String | Amount of asset used to trade                                                                                                                                              |
| currency<mark style="color:red;">\*</mark> | String | The asset used to trade                                                                                                                                                    |
| side<mark style="color:red;">\*</mark>     | String | <p>side of trade: buy or sell.<br><strong>buy</strong>:  the price for buying the base currency.<br><strong>sell</strong>:   the price for selling the quote currency.</p> |
| xid<mark style="color:red;">\*</mark>      | String | External identifier, unique across all resources created under this account.                                                                                               |

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

## Execute a trade

<mark style="color:green;">`POST`</mark> `/v1/conversion/execute`

Execute a trade that has been previously quoted

#### Request Body

| Name                                      | Type   | Description |
| ----------------------------------------- | ------ | ----------- |
| quoteId<mark style="color:red;">\*</mark> | String | Quote ID    |

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
