# 扫码支付

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
示例代码位于 [Github](../#demo-client)
{% endhint %}

## &#x20;提交&#x20;

此 API 会创建扫码支付订单，扣减商户的 USDT 余额，并将资金转入二维码中编码的收款账户。

<mark style="color:green;">`POST`</mark> `/v1/scanPay/submit`

#### 请求 Body

| 名称                                          | 类型            | 说明                                                                                                             |
| --------------------------------------------- | --------------- | ----------------------------------------------------------------------------------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark> | String          | 由合作伙伴提供的交易外部 ID                                                              |
| user\_xid<mark style="color:red;">\*</mark>   | String（最多 20 个字符） | 合作伙伴用于将资金所有者（客户）与交易关联的 ID                                      |
| qrcode<mark style="color:red;">\*</mark>      | String          | 支付二维码。当前支持 _**泰国 PromptPay**._                                                       |
| amount<mark style="color:red;">\*</mark>      | String          | 支付金额。如果二维码包含固定金额，此值必须与二维码中编码的金额**一致**。 |
| notify\_url<mark style="color:red;">\*</mark> | String          | Webhook URL                                                                                                            |

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

<summary>代码示例</summary>

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



## 二维码信息

## 获取指定二维码的详细信息

<mark style="color:green;">`POST`</mark> `/v1/scanPay/info`

#### 请求 Body

| 名称                                     | 类型   | 说明                                                                                                                                                 |
| ---------------------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| qrcode<mark style="color:red;">\*</mark> | String | 支付二维码。当前支持 _**泰国 PromptPay**._                                                                                           |
| amount                                   | String | 支付金额。此值可为 null。但如果二维码包含固定金额，此值必须与二维码中编码的金额**一致**。 |

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





## 查询交易

## 获取指定交易的详细信息

<mark style="color:green;">`POST`</mark> `/v1/order/query`

#### 请求 Body

| 名称                                          | 类型   | 说明                                                |
| --------------------------------------------- | ------ | ---------------------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark> | String | 由合作伙伴提供的交易外部 ID |
| order\_no                                     | String | 要返回的交易 ID                        |

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

