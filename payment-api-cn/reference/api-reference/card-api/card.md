---
description: 创建和查询订单信息。
---

# 卡片

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
示例代码位于 [Github](../#demo-client)
{% endhint %}

## 申请卡片

## 为指定用户发行卡片

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/apply`

每个卡产品只能发行一张卡。

发卡时必须指定 `productId`，它决定要发行的卡产品。卡产品决定卡片类型、卡面、卡片功能、权益、利率和支持的能力等。

#### 请求 Body

| 名称                                                | 类型   | 说明                                                                                                                |
| --------------------------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| user\_id<mark style="color:red;">\*</mark>          | String | 用户 ID 对应一个账户，用于保存卡片消费所需的资金、余额和交易。 |
| request\_id<mark style="color:red;">\*</mark>       | String | 发卡请求的外部标识符。                                                                               |
| card\_product\_id<mark style="color:red;">\*</mark> | String | 要发行的卡片产品 ID                                                                                        |
| card\_level<mark style="color:red;">\*</mark>       | String | 要申请的卡产品等级                                                                                |
| phone\_number<mark style="color:red;">\*</mark>     | String | <p>持卡人手机号码。<br><strong>该手机号码应由合作伙伴预先验证。</strong></p>    |
| phone\_area\_code<mark style="color:red;">\*</mark> | String | 国家/地区电话区号                                                                                                    |
| embossed\_name                                      | String | 卡面上的压印姓名                                                                                             |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    // Response
   "code":200,
   "message":"success",
   "data": {
        "apply_status": "APPLYING",
        "apply_id": "2469990273197955",
        "request_id": "afdsfasf234324"
    }
}
```
{% endtab %}
{% endtabs %}

## 查询申请结果

## 查询卡片申请结果

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/apply-result`

#### 请求 Body

| 名称                                          | 类型   | 说明                                  |
| --------------------------------------------- | ------ | -------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark> | String | 发卡请求的外部标识符。 |
| apply\_id                                     | String | 发卡申请 ID             |
| user\_id<mark style="color:red;">\*</mark>    | String | MuseWallet 中的唯一 ID                  |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "data":{
         "request_id":"2022093002029700786237858945",
         "user_id":"2000061",
         "apply_id":"abc123",
         "card_id":"xxxxx",
         "apply_status":"WAIT_AUDIT"
         },
   "message":"success"
}


```
{% endtab %}
{% endtabs %}

## 获取卡片

## 获取卡片

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/query`

#### 请求 Body

| 名称                                       | 类型   | 说明                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | 已发行卡片的卡片 ID |
| user\_id<mark style="color:red;">\*</mark> | String | MuseWallet 中的唯一 ID    |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "data":{
         "user_id":"2000061",
         "card_id":"xxxxx",
         "phone_number":"1331236",
         "phone_area_code":"86",
         "product_id":"86",
         "card_level":1,
         "card_network":"masterCard",
         "card_type":"physical",
         "currency":"USD",
         "card_no_last4":"0086",
         "card_status":"PENDING_ACTIVE",
         "embossed_name":"coll boston",
         "expiry_month": "04",
         "expiry_year": "2030",
         "issue_time": "13788886666",
         "card_available_balance": 12321,
         "daily_purchaseLimit": 500000,
         "enable_present_transaction": false,
         "enable_noPresent_transaction": true
     }
   "message":"success"
}


```
{% endtab %}
{% endtabs %}

## 激活卡片

## 激活卡片

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/activate`

#### 请求 Body

| 名称                                       | 类型   | 说明                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | 已发行卡片的卡片 ID |
| user\_id<mark style="color:red;">\*</mark> | String | MuseWallet 中的唯一 ID    |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "data":{
         "user_id":"2000061",
         "card_id":"xxxxx",
         "card_status":"PENDING_ACTIVE"
     }
   "message":"success"
}


```
{% endtab %}
{% endtabs %}

## 更新手机号码

## 更新手机号码

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/update-phone`

#### 请求 Body

| 名称                                                | 类型   | 说明                    |
| --------------------------------------------------- | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark>          | String | 已发行卡片的卡片 ID |
| user\_id<mark style="color:red;">\*</mark>          | String | MuseWallet 中的唯一 ID    |
| phone\_number<mark style="color:red;">\*</mark>     | String | 卡片的新手机号码  |
| phone\_area\_code<mark style="color:red;">\*</mark> | String | 国家/地区代码                    |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "data":{
         "user_id":"2000061",
         "card_id":"xxxxx",
         "status":""
     }
   "message":"success"
}


```
{% endtab %}
{% endtabs %}

##

## 锁定卡片

## 锁定卡片

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/lock`

#### 请求 Body

| 名称                                       | 类型   | 说明                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | 已发行卡片的卡片 ID |
| user\_id<mark style="color:red;">\*</mark> | String | MuseWallet 中的唯一 ID    |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "data":{
         "user_id":"2000061",
         "card_id":"xxxxx",
         "card_status":"LOCK"
     }
   "message":"success"
}


```
{% endtab %}
{% endtabs %}

## 解锁卡片

## 解锁卡片

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/unlock`

#### 请求 Body

| 名称                                       | 类型   | 说明                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | 已发行卡片的卡片 ID |
| user\_id<mark style="color:red;">\*</mark> | String | MuseWallet 中的唯一 ID    |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "data":{
         "user_id":"2000061",
         "card_id":"xxxxx",
         "card_status":"ACTIVE"
     }
   "message":"success"
}


```
{% endtab %}
{% endtabs %}

## 获取卡片敏感信息

## 获取卡片敏感信息

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/card-sensitive-info`

生成用于获取卡片敏感信息的短期一次性 URL。返回的 URL 必须由面向客户的应用直接访问，并通过获取请求中提供的客户端 IP 地址访问。

回调 URL 的 API 响应将包含以下 Payload：

`{`&#x20;

&#x20;   `"card_id": "akflf51b3",`&#x20;

&#x20;   `"card_number": "4242424212341234",`&#x20;

&#x20;   `"expiry_month": "11",`&#x20;

&#x20;   `"expiry_year": "2028",`&#x20;

&#x20;   `"security_code": "001"`&#x20;

`}`

#### 请求 Body

| 名称                                          | 类型   | 说明                    |
| --------------------------------------------- | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark>    | String | 已发行卡片的卡片 ID |
| ip\_address<mark style="color:red;">\*</mark> | String | 客户端 IP 地址              |
| user\_id<mark style="color:red;">\*</mark>    | String | MuseWallet 中的唯一 ID    |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "data":{
         "expiry":"2022-09-30", //YYYY-MM-DD
         "url":"https://abc.com/afd" //URL to retrieve card sensitive information
     }
   "message":"success"
}


```
{% endtab %}
{% endtabs %}

## 激活实体卡

## 激活实体卡

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/activate-physical`

#### 请求 Body

| 名称                                       | 类型   | 说明                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | 已发行卡片的卡片 ID |
| user\_id<mark style="color:red;">\*</mark> | String | MuseWallet 中的唯一 ID    |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "data":{
         "user_id":"2000061",
         "card_id":"xxxxx",
         "card_status":"PENDING_ACTIVE"
     }
   "message":"success"
}


```
{% endtab %}
{% endtabs %}

## 修改卡片 PIN

## 获取修改 PIN 的数据

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/get-change-pin-model`

#### 请求 Body

| 名称                                       | 类型   | 说明                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | 已发行卡片的卡片 ID |
| user\_id<mark style="color:red;">\*</mark> | String | MuseWallet 中的唯一 ID    |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "message":"success",
     "cardPinChangeModel":"URL", // URL or API
     "url":"abc.com/change-pin"
}


```
{% endtab %}
{% endtabs %}



## 修改卡片 PIN

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/change-pin`

#### 请求 Body

| 名称                                        | 类型   | 说明                                                                 |
| ------------------------------------------- | ------ | --------------------------------------------------------------------------- |
| card\_id<mark style="color:red;">\*</mark>  | String | 已发行卡片的卡片 ID                                              |
| card\_pin<mark style="color:red;">\*</mark> | String | 新 PIN，仅限 6 位数字，必须使用平台公钥加密 |
| user\_id<mark style="color:red;">\*</mark>  | String | MuseWallet 中的唯一 ID                                                 |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{    
     "code":"200",
     "message":"success"
}


```
{% endtab %}
{% endtabs %}

<details>

<summary>PIN 加密代码示例</summary>

```java
// JAVA
// encrypt(pin, platformPublicKey)
    public static String encrypt(String text, String publicStr) throws Exception {
        PublicKey publicKey = getRSAPublicKey(publicStr);
        Cipher cipher = Cipher.getInstance("RSA");
        cipher.init(Cipher.ENCRYPT_MODE, publicKey);
        byte[] bytes = cipher.doFinal(text.getBytes());
        return Base64Utils.encodeToString(bytes);
    }
    
    @SneakyThrows
    private static RSAPublicKey getRSAPublicKey(String publicKey) {
        publicKey = trim(publicKey);

        KeyFactory kFactory = KeyFactory.getInstance("RSA");
        // decode base64 of your key
        byte[] yourKey =  Base64Utils.decodeFromString(publicKey);
        // generate the public key
        X509EncodedKeySpec spec =  new X509EncodedKeySpec(yourKey);
        return (RSAPublicKey) kFactory.generatePublic(spec);
    }

    private static String trim(String key) {
        return Arrays.stream(key.split("\n"))
                .filter(StringUtils::isNotBlank)
                .map(s -> s.replaceAll("\\s+", ""))
                .filter(i -> !i.startsWith("-----"))
                .collect(Collectors.joining());
    }
```

</details>

## 更换卡片

## 更换卡片

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/replace`

更换为同一卡产品下的新卡

#### 请求 Body

<table><thead><tr><th width="239">名称</th><th>类型</th><th>说明</th></tr></thead><tbody><tr><td>user_id<mark style="color:red;">*</mark></td><td>String</td><td>持卡人的唯一 ID</td></tr><tr><td>original_card_id<mark style="color:red;">*</mark></td><td>String</td><td>原卡片 ID</td></tr><tr><td>replace_reason<mark style="color:red;">*</mark></td><td>String</td><td>换卡原因</td></tr><tr><td>request_id<mark style="color:red;">*</mark></td><td>String</td><td>换卡请求的外部标识符。</td></tr></tbody></table>

**响应**

{% tabs %}
{% tab title="200" %}
```json
{    
     "code":"200",
     "data":{
         "user_id":"6000061",
         "card_id":"xxxxx",
         "card_status":"PENDING_ACTIVE"
     }
   "message":"success"
}
```
{% endtab %}
{% endtabs %}



## 修改卡片消费限额

## 卡片限额

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/limitChange`

修改卡片消费限额

#### 请求 Body

<table><thead><tr><th width="239">名称</th><th>类型</th><th>说明</th></tr></thead><tbody><tr><td>user_id<mark style="color:red;">*</mark></td><td>String</td><td>持卡人的唯一 ID</td></tr><tr><td>card_id<mark style="color:red;">*</mark></td><td>String</td><td>卡片 ID</td></tr><tr><td>daily_purchase_limit<mark style="color:red;">*</mark></td><td>Decimal</td><td>要设置的新每日消费限额</td></tr></tbody></table>

**响应**

{% tabs %}
{% tab title="200" %}
```json
{    
   "code":"200",
   "message":"success"
}
```
{% endtab %}
{% endtabs %}



## 拒绝交易

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/txn-verification-decline`

拒绝交易

#### 请求 Body

<table><thead><tr><th width="239">名称</th><th>类型</th><th>说明</th></tr></thead><tbody><tr><td>user_id<mark style="color:red;">*</mark></td><td>String</td><td>持卡人的唯一 ID</td></tr><tr><td>request_id<mark style="color:red;">*</mark></td><td>String</td><td>请求的外部标识符。</td></tr><tr><td>card_id<mark style="color:red;">*</mark></td><td>String</td><td>卡片 ID</td></tr><tr><td>token<mark style="color:red;">*</mark></td><td>String</td><td>要拒绝的 OOB Token</td></tr></tbody></table>

**响应**

{% tabs %}
{% tab title="200" %}
```json
{    
   "code":"200",
   "message":"success"
}
```
{% endtab %}
{% endtabs %}

## 确认交易

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/txn-verification-confirm`

确认交易

#### 请求 Body

<table><thead><tr><th width="239">名称</th><th>类型</th><th>说明</th></tr></thead><tbody><tr><td>user_id<mark style="color:red;">*</mark></td><td>String</td><td>持卡人的唯一 ID</td></tr><tr><td>request_id<mark style="color:red;">*</mark></td><td>String</td><td>请求的外部标识符。</td></tr><tr><td>card_id<mark style="color:red;">*</mark></td><td>String</td><td>卡片 ID</td></tr><tr><td>token<mark style="color:red;">*</mark></td><td>String</td><td>要确认的 OOB Token</td></tr></tbody></table>

**响应**

{% tabs %}
{% tab title="200" %}
```json
{    
   "code":"200",
   "message":"success"
}
```
{% endtab %}
{% endtabs %}

