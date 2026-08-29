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
