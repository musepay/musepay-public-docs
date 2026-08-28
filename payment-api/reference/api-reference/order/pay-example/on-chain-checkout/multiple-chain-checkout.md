---
description: How to use Checkoutpage to submit a payin.
---

# Multiple Chain Checkout

## Example

```
// crypto order
curl --location --request POST '/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "USDT_BSC", 
    * "amount": "150",
    * "payment_method": "on_line",   
    * "product_name": "product info",
    * "email": "payin@abcpay.io", 
      "notify_url": "https://notify.url",
      "remark": "payout test remark",
    
}'

// Fiat order
curl --location --request POST '/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "IDR",
      "pay_currency": "USDT_BSC", 
    * "amount": "21000",  //fiat amount
    * "payment_method": "on_line",   
    * "product_name": "product info",
      "customer_ref_id": "abc123",
    * "notify_url": "https://notify.url"
    
}'
```

<pre><code>// response
{
  "code":"200",
  "data":      
  {
<strong>    "request_id":"custom_code9982674851738108",
</strong><strong>    "partner_id":"2000051",
</strong><strong>    "order_no":"202406173100230009031352048",
</strong><strong>    "currency":"USDT_BSC",
</strong><strong>    "order_amount":"30",
</strong><strong>    "status":22,
</strong><strong>    "payment_method":"on_line",
</strong><strong>    "receive_address":"0x050b85892F5d5ffffff516868311e7eA2043F",
</strong><strong>    "checkout_url":"https://gateway.dev01.musepay.io/mapi/v1/open/qrCode/CnM1mFBzFDtgr0Er"
</strong><strong>    },
</strong><strong>    "message":"success"
</strong><strong>}
</strong></code></pre>
