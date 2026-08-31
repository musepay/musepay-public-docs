---
description: Query the balance and deposit address of the partner.
---

# Partner

{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](../#demo-client)
{% endhint %}

## Partner Balance

<mark style="color:green;">`POST`</mark> `/v1/balance/partner`

Query the balance of the partner

#### Request Body

| Name                                       | Type   | Description                            |
| ------------------------------------------ | ------ | -------------------------------------- |
| currency<mark style="color:red;">\*</mark> | String | which the balance needs to be queried. |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
  "code": "200",
  "data": {
    "currency": "USDT_TRC20",
    "balance": "100",
    "availableBalance": "100",,
    "freezeBalance": "0",
    "pendingSettleBalance": "0"
  },
  "message": "success"
}
```
{% endtab %}
{% endtabs %}



## Partner Main Address

<mark style="color:green;">`POST`</mark> `/v1/balance/partner-address`

Query the main deposit address of the partner

#### Request Body

| Name                                          | Type   | Description                            |
| --------------------------------------------- | ------ | -------------------------------------- |
| currency<mark style="color:red;">\*</mark>    | String | which the balance needs to be queried. |
| description<mark style="color:red;">\*</mark> | String | description                            |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
  "code": "200",
  "data": {
    "currency": "USDT_ERC20",
    "partner_id": "2001xx34",
    "address": "0x396795DdEFf2119820CddddsfderwfbB1860A",,
    "tag": "",
    "description": "111"
  },
  "message": "success"
}
```
{% endtab %}
{% endtabs %}
