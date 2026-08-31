---
description: >-
  Hosted Checkout mode is the most recommended integration method. Merchants
  only need to create orders, redirect to checkout_url, and handle Webhooks to
  complete payment integration.
---

# Checkout Mode

{% hint style="warning" %}
Every request must contain [common parameters](../../common-parameters.md)
{% endhint %}

### Create checkout order&#x20;

<mark style="color:green;">`POST`</mark>  `/v1/order/pay`

#### Request Body

| Name                | Type   | Description                                                |
| ------------------- | ------ | ---------------------------------------------------------- |
| request\_id\*       | String | The external ID of the transaction provided by the partner |
| payment\_method\*   | String | The way to pay, values: one of \[on\_line, on\_chain]      |
| amount\*            | String | order amount                                               |
| currency\*          | String | order currency                                             |
| remark              | String | The detail information of product in the checkout page     |
| product\_name\*     | String | The product name to be shown in the checkout page          |
| return\_url         | String | web redirect url when payment is finish, if needed         |
| notify\_url         | String | Web-hook url                                               |
| customer\_ref\_id\* | String | customer unique id                                         |
| pay\_currency       | String | The name of crypto asset to pay                            |

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

