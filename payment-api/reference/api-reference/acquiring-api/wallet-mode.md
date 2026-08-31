# Wallet Mode

{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md)
{% endhint %}

## Deposit Address

### Retrieves a deposit address of a specific crypto asset for your end-users.

<mark style="color:green;">`POST`</mark> `/v1/order/deposit_address`

#### Request Body

| Name                | Type   | Description                                                                        |
| ------------------- | ------ | ---------------------------------------------------------------------------------- |
| currency\*          | String | the name of crypto asset to deposit                                                |
| customer\_ref\_id\* | String | The ID for the partner to associate the owner of funds(customer) with transactions |
| description         | String | extend info, don't store any sensitive information                                 |

200: OK

```json
{
    // Response
   "code":200,
   "message":"success",
   "data": {
        "currency": "ETH",
        "address": "0x55d398326f99059fF775485246999027B3197955",
        "tag": ""
    }
}
```

#### Code example

```
// 
curl --location --request POST 'https://api.musepay.io/v1/order/deposit_address' \ 
--header 'Content-Type: application/json' \ 
--data-raw '{ 
    * "partner_id": "2000001", 
    * "sign_type": "RSA", 
    * "timestamp": "1688371190810", 
    * "nonce": "abccefeafjkjsl", 
    * "sign": "examplesignnotcorrect", 
    * "currency": "USDT_BSC", 
    * "customer_ref_id": "USER_123", 
      "description": "" 
    
}'
```

## Query

### Retrieves a specific transaction details

<mark style="color:green;">`POST`</mark>  `/v1/order/query`

#### Request Body

| Name          | Type   | Description                                                |
| ------------- | ------ | ---------------------------------------------------------- |
| request\_id\* | String | The external ID of the transaction provided by the partner |
| order\_no     | String | The ID of the transaction to return                        |

200: OK

```json
{    
     "code":"200", 
     "data":{ 
         "order_no":"2022093020000600011063033204", 
         "request_id":"2022093002029700786237858945", 
         "partner_id":"2000061", 
         "currency":"ETH_TEST", 
         "order_type":"charge", 
         "order_amount":"0.100000000000000000", 
         "arrive_amount":"0.099000000000000000", 
         "fee_amount":"0.001000000000000000", 
         "finish_time":"1664519433", 
         "status":99, 
         "reason":"", 
         "metadata":"{ 
               \"txnHash\": \"0x28f0a68ecd8b88700d7bcaeb62f50bd9d58e0cc8a9c29fb3bd6832868eaac428\", 
               \"networkFee\": \"0.000042000000000000\", 
               \"blockHeight\": \"7684865\", 
               \"description\": \"C100005_descETH_TEST\", 
               \"customerRefId\": \"C100005\", 
               \"numOfConfirms\": \"1\", 
               \"sourceAddress\": \"0xCf441129dC8d91B07fB8cb5122570Bfc607eC471\", 
               \"networkCurrency\": \"ETH_TEST\", 
               \"destinationAddress\": \"0xb4df156e6a10F5DB28E701B79E71Bc2F77B97aa1\" 
               }" 
         }, 
   "message":"success" 
} 
```

## Withdraw

### Submits a new crypto withdraw transaction

<mark style="color:green;">`POST`</mark>  `/v1/order/withdraw`

#### Request Body

| Name                | Type   | Description                                                                        |
| ------------------- | ------ | ---------------------------------------------------------------------------------- |
| request\_id\*       | String | The external ID of the transaction provided by the partner                         |
| currency\*          | String | The name of crypto asset to withdraw                                               |
| address\*           | String | The destination address to withdraw                                                |
| tag                 | String | The withdraw destination tag for Ripple; memo for EOS/XLM                          |
| amount\*            | String | The requested amount to withdraw                                                   |
| notify\_url         | String | Web-hook url                                                                       |
| customer\_ref\_id\* | String | The ID for the partner to associate the owner of funds(customer) with transactions |
| description         | String | extend info, don't store any sensitive information                                 |

200: OK

```json
{ 
 "data": 
 { 
    "order_no":"2022082020000600101063128149", 
    "request_id":"1660977087787", 
    "partner_id":"2000051", 
    "currency":"USDT_TRC20", 
    "address":"0xCf441129dC8d91B07fB8cb5122570Bfc607eC471", 
    "tag":null, 
    "order_amount":"2.200000000000000000", 
    "arrive_amount":"2.178000000000000000", 
    "fee":"0.022000000000000000", 
    "status":22, 
    "fail_reason":"" 
 }, 
 "code":"200", 
 "message":"Success" 
}
```

#### Code example

```
// Some code 

curl --location --request POST 'https://api.musepay.io/v1/order/withdraw 
--header 'Content-Type: application/json' \ 
--data-raw '{ 
    * "partner_id": "2000001", 
    * "sign_type": "RSA", 
    * "timestamp": "1688371190810", 
    * "nonce": "abccefeafjkjsl", 
    * "sign": "examplesignnotcorrect", 
    * "request_id": "custom_code9982674851738108", 
    * "currency": "USDT_BSC", 
    * "customer_ref_id": "USER_123", 
    * "address": "TWVA2tcuA7124a884xuC199sCX8YpUbHFa", 
    * "amount": "150", 
      "notify_url": "https://notify.url", 
      "description": "" 
    
}'
```

## VerifyDepositAddress

### verify an address whether belong to the musepay platform

<mark style="color:green;">`POST`</mark>  `/v1/order/verifyDepositAddress`

#### Request Body

| Name       | Type   | Description                                     |
| ---------- | ------ | ----------------------------------------------- |
| currency\* | String | The name of crypto asset related to the address |
| address\*  | String | The address to verify                           |
| tag        | String | Tag for Ripple; memo for EOS/XLM                |

200: OK

```json
{ 
 "data": 
 { 
    "result": true 
 }, 
 "code":"200", 
 "message":"Success" 
}
```

