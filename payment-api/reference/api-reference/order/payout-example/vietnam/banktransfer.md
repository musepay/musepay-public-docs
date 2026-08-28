# BankTransfer

## Example

```

curl --location --request POST 'https://api.musepay.io/v1/order/payout' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "VND", 
    * "amount": "15000",
    * "settle_currency": "VND", 
    * "payout_method": "bank_transfer",   // fixed value: bank_transfer
    * "bank_code": "1000403", //see support bank code
    * "country": "VN", // fixed value: ID
    * "account_name": "GUILHERME ****** SOUZA",
    * "account_no": "206*****83",
    * "phone": "087*******99",
    * "email": "payout@pay.io", 
    * "notify_url": "https://notify.url",
    * "remark": "payout test remark",
    
}'
```

