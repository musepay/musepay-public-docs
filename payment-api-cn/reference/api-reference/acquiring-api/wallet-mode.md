# Wallet Mode（钱包模式）

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md)
{% endhint %}

## 充值地址

### 为最终用户获取指定数字货币资产的充值地址

<mark style="color:green;">`POST`</mark> `/v1/order/deposit_address`

#### 请求 Body

| 名称                | 类型   | 说明                                                                        |
| ------------------- | ------ | ---------------------------------------------------------------------------------- |
| currency\*          | String | 要充值的数字货币资产名称                                                |
| customer\_ref\_id\* | String | 合作伙伴用于将资金所有者（客户）与交易关联的 ID |
| description         | String | 扩展信息，请勿存储任何敏感信息                                 |

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

#### 代码示例

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

## 查询

### 获取指定交易的详细信息

<mark style="color:green;">`POST`</mark>  `/v1/order/query`

#### 请求 Body

| 名称          | 类型   | 说明                                                |
| ------------- | ------ | ---------------------------------------------------------- |
| request\_id\* | String | 由合作伙伴提供的交易外部 ID |
| order\_no     | String | 要返回的交易 ID                        |

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

## 提现

### 提交新的数字货币提现交易

<mark style="color:green;">`POST`</mark>  `/v1/order/withdraw`

#### 请求 Body

| 名称                | 类型   | 说明                                                                        |
| ------------------- | ------ | ---------------------------------------------------------------------------------- |
| request\_id\*       | String | 由合作伙伴提供的交易外部 ID                         |
| currency\*          | String | 要提现的数字货币资产名称                                               |
| address\*           | String | 提现目标地址                                                |
| tag                 | String | Ripple 的提现目标 Tag；EOS/XLM 的 Memo                          |
| amount\*            | String | 请求提现的金额                                                   |
| notify\_url         | String | Webhook URL                                                                       |
| customer\_ref\_id\* | String | 合作伙伴用于将资金所有者（客户）与交易关联的 ID |
| description         | String | 扩展信息，请勿存储任何敏感信息                                 |

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

#### 代码示例

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

## 验证充值地址

### 验证地址是否属于 MusePay 平台

<mark style="color:green;">`POST`</mark>  `/v1/order/verifyDepositAddress`

#### 请求 Body

| 名称       | 类型   | 说明                                     |
| ---------- | ------ | ----------------------------------------------- |
| currency\* | String | 与该地址相关的数字货币资产名称 |
| address\*  | String | 要验证的地址                           |
| tag        | String | Ripple 的 Tag；EOS/XLM 的 Memo                |

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
