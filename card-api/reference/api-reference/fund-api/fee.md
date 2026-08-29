---
description: Retrieves service fee
---

# Fee

{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](../#demo-client)
{% endhint %}

## Withdraw Coin Fee

## estimate withdraw coin fee

<mark style="color:green;">`POST`</mark> `/v1/fee/estimate`

#### Request Body

| Name                                       | Type   | Description                      |
| ------------------------------------------ | ------ | -------------------------------- |
| currency<mark style="color:red;">\*</mark> | String | the name of crypto asset         |
| amount<mark style="color:red;">\*</mark>   | String | The requested amount to estimate |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    code: '200',
    data: {
      partner_id: '2000051',
      currency: 'TRX',
      fee_amount: '1.1',
      min_threshold: '0',
      decimals: 18
    },
    message: 'success'
  }
```
{% endtab %}
{% endtabs %}

## Query Payout Channel

## Query supported bankCodes and walletCodes

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/fee/queryPayoutChannel`

#### Request Body

| Name                                       | Type   | Description |
| ------------------------------------------ | ------ | ----------- |
| country<mark style="color:red;">\*</mark>  | String |             |
| currency<mark style="color:red;">\*</mark> | String |             |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{"code":"200",
     "data":{
       "banks":
          [{"code":"1000120","enName":"Bank BCA","enShortName":"Bank BCA","localName":"Bank BCA","localShortName":"Bank BCA"},
          {"code":"1000153","enName":"Bank BRI","enShortName":"Bank BRI","localName":"Bank BRI","localShortName":"Bank BRI"}
          ],
       "wallets":
            [{"code":"ovo","enName":"ovo","enShortName":"ovo","localName":"ovo","localShortName":"ovo"},
             {"code":"dana","enName":"dana","enShortName":"dana","localName":"dana","localShortName":"dana"},
             {"code":"linkaja","enName":"LinkAja","enShortName":"LinkAja","localName":"LinkAja","localShortName":"LinkAja"},
             {"code":"gopay","enName":"Gopay","enShortName":"Gopay","localName":"Gopay","localShortName":"Gopay"},
             {"code":"shopeepay","enName":"ShopeePay","enShortName":"ShopeePay","localName":"ShopeePay","localShortName":"ShopeePay"}
             ]
      },
 "message":"success"}
```
{% endtab %}
{% endtabs %}
