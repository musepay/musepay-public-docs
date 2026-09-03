---
description: 与持卡人相关的 API 接口。
---

# 卡用户

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
示例代码位于 [Github](../#demo-client)
{% endhint %}

## **创建用户**

## 使用身份信息创建持卡人

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/create`

#### 请求 Body

| 名称                                                         | 类型   | 说明                                                                                                                                                                                              |
| ------------------------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| user\_xid<mark style="color:red;">\*</mark>                  | String | 外部标识符，在合作伙伴下唯一。                                                                                                                                                           |
| user\_name                                                   | String | 用户账户昵称，为便于阅读的非唯一账户名称                                                                                                                    |
| email<mark style="color:red;">\*</mark>                      | String | 持卡人电子邮箱地址                                                                                                                                                                              |
| individual<mark style="color:red;">\*</mark>                 | Object | 个人持卡人身份信息。                                                                                                                                                             |
| individual.first\_name<mark style="color:red;">\*</mark>     | String | 持卡人的名                                                                                                                                                                                 |
| individual.last\_name<mark style="color:red;">\*</mark>      | String | 持卡人的姓                                                                                                                                                                        |
| individual.date\_of\_birth<mark style="color:red;">\*</mark> | String | 出生日期（YYYY-MM-DD）                                                                                                                                                                               |
| individual.occupation                                        | String | 持卡人职业。                                                                                                                                                                               |
| individual.annual\_income                                    | String | 以卡片币种计算的持卡人年收入                                                                                                                                                            |
| document<mark style="color:red;">\*</mark>                   | Object | 政府签发的身份证件信息                                                                                                                                                    |
| document.type<mark style="color:red;">\*</mark>              | String | 1 或 2，枚举值请参见[证件类型](../../../enums/document-type.md)                                                                                                                                        |
| document.number<mark style="color:red;">\*</mark>            | String | 身份证件号码。                                                                                                                                                                          |
| document.country<mark style="color:red;">\*</mark>           | String | 身份证件签发国，格式为 ISO 3166-1 alpha-2                                                                                                                                   |
| document.expiry\_date<mark style="color:red;">\*</mark>      | String | 身份证件有效期（YYYY-MM-DD）                                                                                                                                                      |
| document.front<mark style="color:red;">\*</mark>             | String | <p>证件正面文件，使用 <strong>data URI Base64 编码格式</strong>。</p><p></p><p>身份证件接受以下 MIME 类型：<br>image/jpeg,<br>image/png。</p><p></p> |
| document.back                                                | String | <p>证件背面文件，使用 data URI Base64 编码格式。</p>                                         |
| document.face                                                | String | <p>自拍照片文件，使用 <strong>data URI Base64 编码格式</strong>。</p><p></p><p>身份证件接受以下 MIME 类型：<br>image/jpeg,<br>image/png。</p>               |
| address                                                      | Object | 配送地址                                                                                                                                                                                         |
| address.country                                              | String | 证件配送国家，格式为 ISO 3166-1 alpha-2                                                                                                                                  |
| address.city                                                 | String | 配送城市                                                                                                                                                                                            |
| address.post\_code                                           | String | 配送邮政编码                                                                                                                                                                                       |
| address.details                                              | String | 详细配送地址                                                                                                                                                                                  |

{% tabs %}
{% tab title="200: OK Success" %}
<pre class="language-javascript"><code class="lang-javascript"><strong>{
</strong>"data":
   { 
    "user_xid":"aabcdfsf",  //user external id       
    "user_id":"8000123",    //user id
    "kyc_status":"0"
   },
"code":"200",
"message":"Success"
}
</code></pre>
{% endtab %}
{% endtabs %}

<details>

<summary>代码示例</summary>

```java
// 
curl --location --request POST 'https://api.musepay.io/v1/carduser/create' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "user_xid": "XUID9982674851738108",
      "user_name": "jasonwood", 
    * "email": "carduser001@musepay.io",     
    * "individual" : {
    *     "first_name": "Jack",
    *     "last_name": "Weather",
    *     "date_of_birth": "1988-02-02",
          "occupation": "01",
          "annual_income":"100000"
      },
      "document": {
    *     "type": "passport",
    *     "number": "G012345678",
    *     "country": "China",
    *     "expiry_date": "2030-10-10",
    *     "front": "afjkfjkasfjajsdfkasfjadsf",
    *     "back": "afjkfjkasfjajsdfkasfjasdafasf"
      },
      "address": {
          "country": "BR",
          "city": "RILA",
          "post_code": "GA1234",
          "details": "No.43 Rd Sky",

      }
}'
```

</details>

## **通过 KYC 链接创建用户**

## 通过 KYC 链接创建持卡人

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/create-with-kyc-link`

#### 请求 Body

| 名称                                        | 类型   | 说明                                                                           |
| ------------------------------------------- | ------ | ------------------------------------------------------------------------------------- |
| email<mark style="color:red;">\*</mark>     | String | 持卡人电子邮箱地址                                                           |
| user\_xid<mark style="color:red;">\*</mark> | String | 外部标识符，在合作伙伴下唯一。                                        |
| user\_name                                  | String | 用户账户昵称，为便于阅读的非唯一账户名称 |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{
"data":
   { 
    "user_xid":"aabcdfsf",  //user external id       
    "user_id":"8000123",    //user id
    "kyc_status":"0",
    "link": "https://aaaa.com/kyc-page"
   },
"code":"200",
"message":"Success"
}
```
{% endtab %}
{% endtabs %}



## **获取用户 KYC 链接**

## 获取用户的 KYC 链接

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/kyc-link`

#### 请求 Body

| 名称                                        | 类型   | 说明                                              |
| ------------------------------------------- | ------ | -------------------------------------------------------- |
| user\_xid<mark style="color:red;">\*</mark> | String | 外部标识符，在合作伙伴下唯一。           |
| level\_name                                 | String | <p>LEVEL-1 或 LEVEL-2。<br>默认值为 LEVEL-1。</p> |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{
"data":
   { 
    "user_xid":"aabcdfsf",  //user external id       
    "link": "https://aaaa.com/kyc-page"
   },
"code":"200",
"message":"Success"
}
```


{% endtab %}
{% endtabs %}





## **获取用户**

## 根据提供的搜索条件获取持卡人集合

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/query`

#### 请求 Body

| 名称                                        | 类型   | 说明 |
| ------------------------------------------- | ------ | ----------- |
| user\_id                                    | String |             |
| phone\_number                               | String |             |
| email                                       | String |             |
| user\_xid<mark style="color:red;">\*</mark> | String |             |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
"data":
   { 
    "user_xid":"aabcdfsf",  //user external id
    "user_id":"8000123",    //user id
    "kyc_status":"0",
    "kyc_level":"1",
    "email": "abc@abc.com",
    "phone_number": "2323",
    "last_name": "abc",
    "first_name": "abc",
    "document_type": "abc",
    "document_number": "aac234"
   },
"code":"200",
"message":"Success"
}
```
{% endtab %}
{% endtabs %}

#### 响应字段

| 名称 | 类型 | 说明 |
| --- | --- | --- |
| kyc\_level | String | 持卡人当前的 KYC 等级。 |

## 上传用户 KYC

## 上传用户 KYC 信息

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/upload-kyc`

#### 请求 Body

| 名称                                                         | 类型   | 说明                                                                                                                                                                                              |
| ------------------------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| user\_xid<mark style="color:red;">\*</mark>                  | String | 外部标识符，在合作伙伴下唯一。                                                                                                                                                           |
| individual<mark style="color:red;">\*</mark>                 | Object | 个人持卡人身份信息。                                                                                                                                                             |
| individual.first\_name<mark style="color:red;">\*</mark>     | String | 持卡人的名                                                                                                                                                                                 |
| individual.last\_name<mark style="color:red;">\*</mark>      | String | 持卡人的姓                                                                                                                                                                        |
| individual.date\_of\_birth<mark style="color:red;">\*</mark> | String | 出生日期（YYYY-MM-DD）                                                                                                                                                                               |
| individual.occupation                                        | String | 持卡人职业。                                                                                                                                                                               |
| individual.annual\_income                                    | String | 以卡片币种计算的持卡人年收入                                                                                                                                                            |
| document<mark style="color:red;">\*</mark>                   | Object | 政府签发的身份证件信息                                                                                                                                                    |
| document.type<mark style="color:red;">\*</mark>              | String | 1 或 2，枚举值请参见[证件类型](../../../enums/document-type.md)                                                                                                                                        |
| document.number<mark style="color:red;">\*</mark>            | String | 身份证件号码。                                                                                                                                                                          |
| document.country<mark style="color:red;">\*</mark>           | String | 身份证件签发国，格式为 ISO 3166-1 alpha-2                                                                                                                                   |
| document.expiry\_date<mark style="color:red;">\*</mark>      | String | 身份证件有效期（YYYY-MM-DD）                                                                                                                                                      |
| document.front<mark style="color:red;">\*</mark>             | String | <p>证件正面文件，使用 <strong>data URI Base64 编码格式</strong>。</p><p></p><p>身份证件接受以下 MIME 类型：<br>image/jpeg,<br>image/png。</p><p></p> |
| document.back                                                | String | <p>证件背面文件，使用 data URI Base64 编码格式。</p>                                         |
| address                                                      | Object | 配送地址                                                                                                                                                                                         |
| address.country                                              | String | 证件配送国家，格式为 ISO 3166-1 alpha-2                                                                                                                                  |
| address.city                                                 | String | 配送城市                                                                                                                                                                                            |
| address.post\_code                                           | String | 配送邮政编码                                                                                                                                                                                       |
| address.details                                              | String | 详细配送地址                                                                                                                                                                                  |

{% tabs %}
{% tab title="200: OK Success" %}
<pre class="language-javascript"><code class="lang-javascript"><strong>{
</strong>"data":
   { 
    "user_xid":"aabcdfsf",  //user external id       
    "user_id":"8000123",    //user id
    "kyc_status":"0"
   },
"code":"200",
"message":"Success"
}
</code></pre>
{% endtab %}
{% endtabs %}



## 修改用户电子邮箱

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/change-email`

更新用户电子邮箱时，如果用户已有卡片，卡片关联的电子邮箱也会同步更新。&#x20;

#### 请求 Body

| 名称     | 类型   | 说明                     |
| -------- | ------ | ------------------------------- |
| user\_id | String | 用户唯一 ID                  |
| email    | String | 持卡人的新电子邮箱地址 |

**响应**

{% tabs %}
{% tab title="200" %}
```json
{
  "success": true
}
```
{% endtab %}
{% endtabs %}
