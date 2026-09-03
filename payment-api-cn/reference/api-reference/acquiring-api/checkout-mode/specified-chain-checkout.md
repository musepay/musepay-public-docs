# 指定链收银台

## 示例

```bash
// crypto order
curl --location --request POST '/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "USDT_BSC_TEST", 
    * "amount": "150",
    * "payment_method": "on_chain",   
    * "product_name": "product info",
      "customer_ref_id": "abc123",
    * "notify_url": "https://notify.url",
      "remark": ""
    
}'



// Fiat order
curl --location --request POST '/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "IDR",
      "pay_currency": "USDT_BSC_TEST", 
    * "amount": "210",
    * "payment_method": "on_chain",   
    * "product_name": "product info",
      "customer_ref_id": "abc123",
    * "notify_url": "https://notify.url"
    
}'
```

```json
// response
{
  "code":"200",
  "data": {
    "request_id":"custom_code9982674851738108",
    "partner_id":"2000051",
    "order_no":"202406173100230009031352048",
    "currency":"USDT_BSC_TEST",
    "order_amount":"30",
    "status":22,
    "payment_method":"on_chain",
    "receive_address":"0x050b85892F5d5ffffff516868311e7eA2043F",
    "checkout_url":"https://gateway.dev01.musepay.io/mapi/v1/open/qrCode/CnM1mFBzFDtgr0Er"
  },
  "message":"success"
}
```
