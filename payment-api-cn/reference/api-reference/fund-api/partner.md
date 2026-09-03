---
description: 查询合作伙伴的余额和充值地址。
---

# 合作伙伴

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
示例代码位于 [Github](../#demo-client)
{% endhint %}

## 合作伙伴余额

<mark style="color:green;">`POST`</mark> `/v1/balance/partner`

查询合作伙伴余额

#### 请求 Body

| 名称                                       | 类型   | 说明                            |
| ------------------------------------------ | ------ | -------------------------------------- |
| currency<mark style="color:red;">\*</mark> | String | 需要查询余额的币种。 |

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



## 合作伙伴主地址

<mark style="color:green;">`POST`</mark> `/v1/balance/partner-address`

查询合作伙伴的主充值地址

#### 请求 Body

| 名称                                          | 类型   | 说明                            |
| --------------------------------------------- | ------ | -------------------------------------- |
| currency<mark style="color:red;">\*</mark>    | String | 需要查询余额的币种。 |
| description<mark style="color:red;">\*</mark> | String | 说明                                 |

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
