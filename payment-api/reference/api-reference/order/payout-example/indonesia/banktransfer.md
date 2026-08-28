---
description: How to use bank transfer to submit a payout in Indonesia.
---

# BankTransfer

## Example

```

curl --location --request POST 'https://api.musepay.io/v1/order/payout' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "USDT_TRC20", 
    * "amount": "150",
    * "settle_currency": "IDR", // fixed value: IDR
    * "payout_method": "bank_transfer",   // fixed value: bank_transfer
    * "bank_code": "1000120", //see support bank code
    * "country": "ID", // fixed value: ID
    * "account_name": "GUILHERME ****** SOUZA",
    * "account_no": "206*****83",
    * "phone": "087*******99",
    * "email": "payout@pay.io", 
    * "notify_url": "https://notify.url",
    * "remark": "payout test remark",
    
}'
```
