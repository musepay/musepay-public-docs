---
description: create and query order information .
---

# Order

{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](../#demo-client)
{% endhint %}

## Deposit\_address

## Retrieves a deposit address of a specific crypto asset

<mark style="color:green;">`POST`</mark> `/v1/order/deposit_address`

#### Request Body

| Name                                                | Type   | Description                                                                        |
| --------------------------------------------------- | ------ | ---------------------------------------------------------------------------------- |
| currency<mark style="color:red;">\*</mark>          | String | the name of crypto asset to deposit                                                |
| customer\_ref\_id<mark style="color:red;">\*</mark> | String | The ID for the partner to associate the owner of funds(customer) with transactions |
| description                                         | String | extend info, don't store any sensitive information                                 |

{% tabs %}
{% tab title="200: OK " %}
```javascript
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
{% endtab %}
{% endtabs %}

<details>

<summary>Code example</summary>

<pre class="language-javascript"><code class="lang-javascript"><strong>// 
</strong>curl --location --request POST 'https://api.musepay.io/v1/order/deposit_address' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "partner_id": "2000001", 
    * "sign_type": "RSA", 
<strong>    * "timestamp": "1688371190810", 
</strong>    * "nonce": "abccefeafjkjsl", 
    * "sign": "examplesignnotcorrect", 
    * "currency": "USDT_BSC", 
    * "customer_ref_id": "USER_123",
      "description": ""
    
}'

</code></pre>

</details>



## Query

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
{% endtab %}
{% endtabs %}



## Withdraw

## Submits a new withdraw transaction

<mark style="color:green;">`POST`</mark> `/v1/order/withdraw`

#### Request Body

| Name                                                | Type   | Description                                                                        |
| --------------------------------------------------- | ------ | ---------------------------------------------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark>       | String | The external ID of the transaction provided by the partner                         |
| currency<mark style="color:red;">\*</mark>          | String | The name of crypto asset to withdraw                                               |
| address<mark style="color:red;">\*</mark>           | String | The destination address to withdraw                                                |
| tag                                                 | String | The withdraw destination tag for Ripple; memo for EOS/XLM                          |
| amount<mark style="color:red;">\*</mark>            | String | The requested amount to withdraw                                                   |
| notify\_url                                         | String | Web-hook url                                                                       |
| customer\_ref\_id<mark style="color:red;">\*</mark> | String | The ID for the partner to associate the owner of funds(customer) with transactions |
| description                                         | String | extend info, don't store any sensitive information                                 |

{% tabs %}
{% tab title="200: OK " %}
```java
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
{% endtab %}
{% endtabs %}

<details>

<summary>Code example</summary>

```javascript
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

</details>

## VerifyDepositAddress

## verify an address whether belong to the platform

<mark style="color:green;">`POST`</mark> `/v1/order/verifyDepositAddress`

#### Request Body

| Name                                       | Type   | Description                                     |
| ------------------------------------------ | ------ | ----------------------------------------------- |
| currency<mark style="color:red;">\*</mark> | String | The name of crypto asset related to the address |
| address<mark style="color:red;">\*</mark>  | String | The address to verify                           |
| tag                                        | String | Tag for Ripple; memo for EOS/XLM                |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
 "data":
 {
    "result": true
 },
 "code":"200",
 "message":"Success"
}
```
{% endtab %}
{% endtabs %}

## Pay

## allow to submit a payin by checkout page or direct integration

<mark style="color:green;">`POST`</mark> `/v1/order/pay`

#### Request Body

| Name                                                | Type       | Description                                                                       |
| --------------------------------------------------- | ---------- | --------------------------------------------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark>       | String     | The external ID of the transaction provided by the partner                        |
| payment\_method<mark style="color:red;">\*</mark>   | String     | The way to pay, values: one of \[on\_line, direct,on\_chain]                      |
| amount<mark style="color:red;">\*</mark>            | String     | order amount                                                                      |
| currency<mark style="color:red;">\*</mark>          | String     | order currency                                                                    |
| remark                                              | String     | The detail information of product in the checkout page                            |
| product\_name<mark style="color:red;">\*</mark>     | String     | The product name to be shown in the checkout page                                 |
| return\_url                                         | String     | web redirect url when payment is finish, if needed                                |
| notify\_url                                         | String     | Web-hook url                                                                      |
| customer.email                                      | String     | The e-mail address of customer                                                    |
| customer.phone                                      | String     | The phone number of customer                                                      |
| payment\_channel                                    | String     | required if payment method is direct, see [_Enums_](../../../enums/payment-type/) |
| payment\_type                                       | String     | required if payment method is direct, see [Enums](../../../enums/payment-type/)   |
| customer.name                                       | String     | customer name                                                                     |
| customer\_ref\_id<mark style="color:red;">\*</mark> | String     | customer unique id                                                                |
| pay\_currency                                       | String     | The name of crypto asset to pay                                                   |
| customer                                            | JSONString | customer info                                                                     |

{% tabs %}
{% tab title="200: OK when payment_method = on_line" %}
```json
{"code":"200",
 "data":{
   "request_id":"1675157000687",
   "partner_id":"2000051",
   "order_no":"2023013120000600262092321146",
   "currency":"USDT_TRC20",
   "order_amount":"0.3",
   "status":11,
   "payment_method":"on_line",
   "checkout_url":"http://api.dev.xx/v1/qrcode/CnHmkPayhcIFlyat"
 },
 "message":"success"
 }
```
{% endtab %}

{% tab title="200: OK when payment_method = direct" %}
```json
{"code":"200",
 "data":{
   "request_id":"1675157000687",
   "partner_id":"2000051",
   "order_no":"2023013120000600262092321146",
   "currency":"IDR",
   "order_amount":"0.3",
   "status":11,
   "payment_method":"direct",
   "checkout_url":"http://api.dev.musepay.io/v1/qrcode/CnHmkPayhcIFlyat",
   "wallet_url":"http://ovo.com/vfsjdkfdst",
   "qrcode_string":"abccddafdsfdasfsfas",
   "account_name":"BCA",
   "account_number":"2342432434343",
   "account_type":"virtual_account", 
 },
 "message":"success"
 }
```
{% endtab %}

{% tab title="200: OK when payment_method = on_chain" %}
```json
{"code":"200",
 "data":{
   "request_id":"1675157000687",
   "partner_id":"2000051",
   "order_no":"2023013120000600262092321146",
   "currency":"USDT_TRC20",
   "order_amount":"0.3",
   "status":11,
   "payment_method":"on_chain",
   "receive_address":"0x5635320sfs4BD3a9cA99bE6e20906Ec53d1Ca65ad"
 },
 "message":"success"
 }
```
{% endtab %}
{% endtabs %}

{% content-ref url="pay-example/" %}
[pay-example](pay-example/)
{% endcontent-ref %}

## Payout

## allow to submit a payout request

<mark style="color:green;">`POST`</mark>`/v1/order/payout`

#### Request Body

| Name                                               | Type   | Description                                                                                 |
| -------------------------------------------------- | ------ | ------------------------------------------------------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark>      | String | The external ID of the transaction provided by the partner                                  |
| account\_type                                      | String | <p>required if payout_method is wallet_transfer</p><p>-one of[ PHONE, EMAIL,CPF, CNPJ ]</p> |
| account\_no<mark style="color:red;">\*</mark>      | String | Beneficiary's account No                                                                    |
| account\_name<mark style="color:red;">\*</mark>    | String | <p>Beneficiary's name<br>-Min 5 , Max 100 -</p>                                             |
| country<mark style="color:red;">\*</mark>          | String | country code                                                                                |
| bank\_code                                         | String | required if payout\_method is bank\_transfer                                                |
| wallet\_code                                       | String | required if payout\_method is wallet\_transfer                                              |
| payout\_method<mark style="color:red;">\*</mark>   | String | One of \[bank\_transfer \| wallet\_transfer]                                                |
| settle\_currency<mark style="color:red;">\*</mark> | String | The currency to receive                                                                     |
| amount<mark style="color:red;">\*</mark>           | String | Merchant's Payout Amount                                                                    |
| currency<mark style="color:red;">\*</mark>         | String | Merchant's account currency                                                                 |
| remark                                             | String | <p>Payout Remark</p><p>- Max length: 40 - </p>                                              |
| bank\_routing\_code                                | String | <p>Bank Routing Code</p><p>- Max length: 100 - </p>                                         |
| document\_type                                     | String | Identification type                                                                         |
| document\_id                                       | String | Identification number                                                                       |
| phone<mark style="color:red;">\*</mark>            | String | Beneficiary's phone.                                                                        |
| email<mark style="color:red;">\*</mark>            | String | Beneficiary's email                                                                         |
| notify\_url                                        | String | web redirect url when payment is finish,if needed                                           |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{"code":"200",
 "data":{
   "request_id":"1675157000687",
   "partner_id":"2000051",
   "order_no":"2023013120000600262092321146",
   "currency":"USDT_TRC20",
   "order_amount":"0.3",
   "status":11
 },
 "message":"success"
 }
```
{% endtab %}
{% endtabs %}

{% content-ref url="payout-example/" %}
[payout-example](payout-example/)
{% endcontent-ref %}
