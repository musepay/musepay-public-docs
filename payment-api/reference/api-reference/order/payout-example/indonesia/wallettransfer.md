---
description: How to use a third party wallet to submit a payout in Indonesia.
---

# WalletTransfer

## Example

```

curl --location --request POST 'https://api.musepay.io/v1/order/payout' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "USDT_TRC20", 
    * "amount": "150",
    * "settle_currency": "IDR", // fixed value: IDR
    * "payout_method": "wallet_transfer",   // fixed value: wallet_transfer
    * "wallet_code": "ovo", //see support wallet code
    * "country": "ID", // fixed value: ID
    * "account_name": "GUILHERME ****** SOUZA",
    * "account_no": "087*******99",
    * "account_type": "PHONE",  // should be one of PHONE EMAIL 
    * "phone": "087*******99",
    * "email": "payout@pay.io", 
    * "notify_url": "https://notify.url",
    * "remark": "payout test remark",
    
}'
```
