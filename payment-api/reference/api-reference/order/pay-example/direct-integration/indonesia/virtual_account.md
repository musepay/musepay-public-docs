# Virtual\_account

## Example

```
// 
curl --location --request POST 'https://api.musepay.io/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
      "pay_currency": "IDR",
    * "currency": "IDR", 
    * "amount": "150",
    * "payment_method": "direct",   
    * "payment_type": "virtual_account",   
    * "payment_channel": "1000120",   //see support virtual account code
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
   "currency":"IDR",
   "order_amount":"0.3",
   "status":11,
   "payment_method":"direct",
   "checkout_url":"http://api.fff/v1/qrcode/CnHmkPayhcIFlyat",
   "account_name":"BCA",
   "account_number":"2342432434343",
   "account_type":"virtual_account", 
 },
 "message":"success"
 }
```
