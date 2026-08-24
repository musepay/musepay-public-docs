# Query Order

{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md)
{% endhint %}

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

