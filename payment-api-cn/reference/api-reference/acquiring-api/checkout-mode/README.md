---
description: >-
  托管收银台模式是最推荐的集成方式。商户
  只需创建订单、重定向到 checkout_url，并处理 Webhook，即可
  完成支付集成。
---

# Checkout Mode（收银台模式）

{% hint style="warning" %}
每个请求都必须包含[通用参数](../../common-parameters.md)
{% endhint %}

### 创建收银台订单&#x20;

<mark style="color:green;">`POST`</mark>  `/v1/order/pay`

#### 请求 Body

| 名称                | 类型   | 说明                                                |
| ------------------- | ------ | ---------------------------------------------------------- |
| request\_id\*       | String | 由合作伙伴提供的交易外部 ID |
| payment\_method\*   | String | 支付方式，可选值为 \[on\_line, on\_chain] 之一      |
| amount\*            | String | 订单金额                                               |
| currency\*          | String | 订单币种                                             |
| remark              | String | 收银台页面中的商品详细信息     |
| product\_name\*     | String | 收银台页面中显示的商品名称          |
| return\_url         | String | 支付完成后的网页重定向 URL（如需）         |
| notify\_url         | String | Webhook URL                                               |
| customer\_ref\_id\* | String | 客户唯一 ID                                         |
| pay\_currency       | String | 用于支付的数字货币资产名称                            |

200: OK&#x20;

```json
{"code":"200", 
 "data":{ 
   "request_id":"1675157000687", 
   "partner_id":"2000051", 
   "order_no":"2023013120000600262092321146", 
   "currency":"USDT_TRC20", 
   "order_amount":"0.3", 
   "status":11, 
   "payment_method":"on_line", 
   "checkout_url":"http://api.dev.xx/v1/qrcode/CnHmkPayhcIFlyat" ,
   "receive_address":"0x5635320sfs4BD3a9cA99bE6e20906Ec53d1Ca65ad" 
 }, 
 "message":"success" 
 }
```
