# WalletTransfer

## Example

```

curl --location --request POST 'https://api.musepay.io/v1/order/payout' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "PHP", 
    * "amount": "150",
    * "settle_currency": "PHP", // fixed value: PHP
    * "payout_method": "wallet_transfer",   // fixed value: wallet_transfer
    * "wallet_code": "2000506", //see support wallet code
    * "country": "PH", 
    * "account_name": "GUILHERME ****** SOUZA",
    * "account_no": "087*******99",
    * "account_type": "PHONE",  // should be one of PHONE EMAIL 
    * "phone": "087*******99",
    * "email": "payout@pay.io", 
    * "notify_url": "https://notify.url",
    * "remark": "payout test remark",
    
}'
```
