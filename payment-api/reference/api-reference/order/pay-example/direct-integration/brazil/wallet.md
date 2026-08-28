# Wallet

Example

<pre><code><strong>// Request
</strong>curl --location --request POST 'https://api.musepay.io/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
      "pay_currency": "BRL",
    * "currency": "BRL", 
    * "amount": "150",
    * "payment_method": "direct",   
    * "payment_type": "wallet",   
    * "payment_channel": "pix",   //see support wallet code
    * "product_name": "product info",
    * "customer_ref_id": "abcd1234",
    * "customer" : {
    *     "name": "Test User Name",
    *     "phone": "087*******99",
    *     "email": "test@padsf.com",
    *     "document_id": "123345544664",
    *     "document_type": "CPF" // CPF 
      },
      "notify_url": "https://notify.url",
      "remark": "payout test remark",
    
}'
</code></pre>

```
// Response

{"code":"200",
 "data":{
   "request_id":"1675157000687",
   "partner_id":"2000051",
   "order_no":"2023013120000600262092321146",
   "currency":"BRL",
   "order_amount":"0.3",
   "status":11,
   "payment_method":"direct",
   "wallet_url":"http://pix.com/vfsjdkfdst",
   "checkout_url":"http://pix.com/vfsjdkfdst"
 },
 "message":"success"
 }
```

