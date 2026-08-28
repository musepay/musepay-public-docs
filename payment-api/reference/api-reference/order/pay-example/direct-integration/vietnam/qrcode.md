# Qrcode

## Example

```
// request
curl --location --request POST 'https://api.musepay.io/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
      "pay_currency": "VND",
    * "currency": "VND", 
    * "amount": "150000",
    * "payment_method": "direct",   
    * "payment_type": "qrcode",   
    * "payment_channel": "1000433",   //see support qrcode code
    * "product_name": "product info",
    * "customer_ref_id": "abcd1234",
      "notify_url": "https://notify.url",
      "remark": "payout test remark",
    
}'
```

```
// response

{"code":"200",
 "data":{
   "request_id":"1675157000687",
   "partner_id":"2000051",
   "order_no":"2023013120000600262092321146",
   "currency":"VND",
   "order_amount":"150000",
   "status":11,
   "payment_method":"direct",
   "checkout_url":"https://dne/bankdken=Mx5rbTdKpGLseRfJdA%3D%3D&id=13982054"
 },
 "message":"success"
 }
```
