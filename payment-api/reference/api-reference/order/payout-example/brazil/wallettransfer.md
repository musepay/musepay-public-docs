---
description: How to use a third party wallet to submit a payout in Brazil.
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
    * "settle_currency": "BRL", // fixed value: BRL
    * "payout_method": "wallet_transfer",   // fixed value: wallet_transfer
    * "wallet_code": "pix",
    * "country": "BR", // fixed value: BR
    * "account_name": "GUILHERME ****** SOUZA",
    * "account_no": "22*******99",
    * "account_type": "CPF",  //  CPF，EMAIL，PHONE
    * "phone": "123456789123", // 11 digits
    * "email": "payout@pay.io",
    * "document_id": "22*******99",
    * "document_type": "CPF", //fixed value
    * "notify_url": "https://notify.url",
    * "remark": "payout test remark",
    
}'
```
