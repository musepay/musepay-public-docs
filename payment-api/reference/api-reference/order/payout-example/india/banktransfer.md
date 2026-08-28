# BankTransfer

## Example

```

curl --location --request POST 'https://api.musepay.io/v1/order/payout' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "INR", 
    * "amount": "15000",
    * "settle_currency": "INR", 
    * "payout_method": "bank_transfer",   // fixed value: bank_transfer
    * "bank_code": "bank_card", //see support bank code
    * "country": "IN", 
    * "account_name": "Suvidhaa",
    * "account_no": "397505***09",
    * "phone": "087*******99",
    * "email": "payout@pay.io", 
    * "document_id": "ICIC000397",  //IFSC 
    * "document_type": "IFSC",
    * "notify_url": "https://notify.url",
    * "remark": "payout test remark",
    
}'
```
