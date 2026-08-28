# Wallet

Example

```
// Request
curl --location --request POST 'https://api.musepay.io/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
      "pay_currency": "INR",
    * "currency": "INR", 
    * "amount": "150",
    * "payment_method": "direct",   
    * "payment_type": "wallet",   
    * "payment_channel": "upi",   //see support wallet code
    * "product_name": "product info",
    * "customer_ref_id": "abcd1234",
    * "customer" : {
    *     "name": "Test User Name",
    *     "phone": "087*******99",
    *     "email": "test@pagsmile.com",
      },
      "notify_url": "https://notify.url",
      "remark": "payout test remark",
    
}'
```

```
// Response

{"code":"200",
 "data":{
   "request_id":"1675157000687",
   "partner_id":"2000051",
   "order_no":"2023013120000600262092321146",
   "currency":"INR",
   "order_amount":"30",
   "status":11,
   "payment_method":"direct",
   "wallet_url":"https://api.xxx.com/payment/upi.webapp?f=20231204102yp1UG3iZz"
 },
 "message":"success"
 }
```
