---
description: Retrieves the balance information on a specific asset.
---

# Balance

{% hint style="warning" %}
Every request must contain [common parameters](common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](./#demo-client)
{% endhint %}

## **Partner balance**

## partner account balance

<mark style="color:green;">`POST`</mark> `/v1/balance/partner`

#### Request Body

| Name                                       | Type   | Description                                |
| ------------------------------------------ | ------ | ------------------------------------------ |
| currency<mark style="color:red;">\*</mark> | String | the name of crypto asset to return balance |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
"data":
   { 
    "currency":"TRX",        
    "balance":"0.200000000000000000",
    "availableBalance":"0.200000000000000000",
    "freezeBalance":"0.000000000000000000",
    "pendingSettleBalance":"0"
   },
"code":"200",
"message":"Success"
}
```
{% endtab %}
{% endtabs %}

<details>

<summary>Code example</summary>

```java
// Some code
String respStr = client.queryPartnerBalance(
                "USDT_TRC20",                                //currency
                "2000051",                                   //partner_id
                String.valueOf(System.currentTimeMillis())   //nonce
                );
 System.out.println(respStr);
```

</details>

