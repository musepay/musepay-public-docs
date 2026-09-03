---
description: 获取服务费
---

# 费用

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
示例代码位于 [Github](../#demo-client)
{% endhint %}

## 数字货币提现费用

## 估算数字货币提现费用

<mark style="color:green;">`POST`</mark> `/v1/fee/estimate`

#### 请求 Body

| 名称                                       | 类型   | 说明                      |
| ------------------------------------------ | ------ | -------------------------------- |
| currency<mark style="color:red;">\*</mark> | String | 数字货币资产名称         |
| amount<mark style="color:red;">\*</mark>   | String | 请求估算的金额 |

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
