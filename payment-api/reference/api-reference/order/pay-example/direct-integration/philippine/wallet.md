# Wallet

## Example

```
// request
curl --location --request POST 'https://api.musepay.io/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "PHP", 
    * "amount": "150",
    * "payment_method": "direct",   
    * "payment_type": "wallet",   
    * "payment_channel": "2000506",   //see support wallet code
    * "product_name": "product info",
    * "customer_ref_id": "abcd1234",
    * "customer_ref_id": "abcd1234",
      "notify_url": "https://notify.url",
      "remark": " test remark",
    
}'
```

```
// response

{"code":"200",
 "data":{
   "request_id":"1675157000687",
   "partner_id":"2000051",
   "order_no":"2023013120000600262092321146",
   "currency":"PHP",
   "order_amount":"0.3",
   "status":11,
   "payment_method":"direct",
   "wallet_url":"http://dddd.com/vfsjdkfdst"
 },
 "message":"success"
 }
```
