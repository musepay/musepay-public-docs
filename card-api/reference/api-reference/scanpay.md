---
description: >-
  This chapter provides the API specifications for creating and querying
  Scan-to-Pay orders.
---

# ScanPay

{% hint style="warning" %}
Every request must contain [common parameters](common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](./#demo-client)
{% endhint %}

## &#x20;Submit&#x20;

This API creates a Scan-to-Pay order, deducts the merchant’s USDT balance, and transfers the funds to the payee account encoded in the QR code.

<mark style="color:green;">`POST`</mark> `/v1/scanPay/submit`

#### Request Body

| Name                                          | Type            | Description                                                                                                             |
| --------------------------------------------- | --------------- | ----------------------------------------------------------------------------------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark> | String          | The external ID of the transaction provided by the partner                                                              |
| user\_xid<mark style="color:red;">\*</mark>   | String (max.20) | The ID for the partner to associate the owner of funds(customer) with transactions                                      |
| qrcode<mark style="color:red;">\*</mark>      | String          | The payment QR code. Currently supports _**Thailand PromptPay**._                                                       |
| amount<mark style="color:red;">\*</mark>      | String          | The payout amount. If the QR code contains a fixed amount, this value must **match the amount** encoded in the QR code. |
| notify\_url<mark style="color:red;">\*</mark> | String          | Web-hook url                                                                                                            |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    // Response
   "code":200,
   "message":"success",
   "data": {
        "orderNo": "20012332r42723478324",
        "status": 22
    }
}
```
{% endtab %}
{% endtabs %}

<details>

<summary>Code example</summary>

<pre class="language-javascript"><code class="lang-javascript"><strong>// 
</strong>curl --location --request POST 'https://api.musepay.io/v1/scanPay/submit' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "partner_id": "2000001", 
    * "sign_type": "RSA", 
<strong>    * "timestamp": "1688371190810", 
</strong>    * "nonce": "abccefeafjkjsl", 
    * "sign": "examplesignnotcorrect", 
    * "request_id": "abc12347465746", 
    * "user_xid": "USER_123",
    * "qrcode": "00020101021229370016A000000677010111011300666102576555802TH530376454044.22630464C9",
    * "amount": "100",
    * "notify_url": "https://google.com"
}'

</code></pre>

</details>



## Qrcode Info

## Retrieves a specific Qrcode details

<mark style="color:green;">`POST`</mark> `/v1/scanPay/info`

#### Request Body

| Name                                     | Type   | Description                                                                                                                                                 |
| ---------------------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| qrcode<mark style="color:red;">\*</mark> | String | The payment QR code. Currently supports _**Thailand PromptPay**._                                                                                           |
| amount                                   | String | The payout amount.  This value can be null.  However, If the QR code contains a fixed amount, this value must **match the amount** encoded in the QR code.  |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
  "code": "200",
  "data": {
    "qrcode_type": "prompt_pay",
    "amount": "32",
    "currency": "THB",
    "order_amount": "1.0043942247",
    "order_currency": "USDT",
    "fee_amount": "1",
    "fee_currency": "USDT",
    "exchange_rate": "31.86",
    "beneficiary_name": null,
    "account_type": null,
    "bank_code": null,
    "bank_name": null
  },
  "message": "success"
}
```
{% endtab %}
{% endtabs %}





## Query transaction

## Retrieves a specific transaction details

<mark style="color:green;">`POST`</mark> `/v1/order/query`

#### Request Body

| Name                                          | Type   | Description                                                |
| --------------------------------------------- | ------ | ---------------------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark> | String | The external ID of the transaction provided by the partner |
| order\_no                                     | String | The ID of the transaction to return                        |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{    
     "code":"200",
     "data":{
         "order_no":"2022093020000600011063033204",
         "request_id":"2022093002029700786237858945",
         "partner_id":"2000061",
         "currency":"ETH_TEST",
         "order_type":"proxy_pay",
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
{% endtab %}
{% endtabs %}

