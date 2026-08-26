---
description: API endpoints pertaining to the cardholder.
---

# Card User

{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](../#demo-client)
{% endhint %}

## **Create User**

## Create a cardholder with identity information

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/create`

#### Request Body

| Name                                                         | Type   | Description                                                                                                                                                                                              |
| ------------------------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| user\_xid<mark style="color:red;">\*</mark>                  | String | External identifier, unique under the partner.                                                                                                                                                           |
| user\_name                                                   | String | Nickname of user account, this is a human-friendly non-unique name for a user account                                                                                                                    |
| email<mark style="color:red;">\*</mark>                      | String | Email address of cardholder                                                                                                                                                                              |
| individual<mark style="color:red;">\*</mark>                 | Object | Individual card holder identity information.                                                                                                                                                             |
| individual.first\_name<mark style="color:red;">\*</mark>     | String | First name of cardholder                                                                                                                                                                                 |
| individual.last\_name<mark style="color:red;">\*</mark>      | String | Last name / Surname of cardholder                                                                                                                                                                        |
| individual.date\_of\_birth<mark style="color:red;">\*</mark> | String | Date of birth (YYYY-MM-DD)                                                                                                                                                                               |
| individual.occupation                                        | String | Occupation of card holder.                                                                                                                                                                               |
| individual.annual\_income                                    | String | Annual income of card holder in card currency                                                                                                                                                            |
| document<mark style="color:red;">\*</mark>                   | Object | Government Issued Identification Document Information                                                                                                                                                    |
| document.type<mark style="color:red;">\*</mark>              | String | 1 or 2, enums in [Document Type](../../../enums/document-type.md)                                                                                                                                        |
| document.number<mark style="color:red;">\*</mark>            | String | Identification document number.                                                                                                                                                                          |
| document.country<mark style="color:red;">\*</mark>           | String | Issuing country of identification document in ISO3166-1 alpha-2 format                                                                                                                                   |
| document.expiry\_date<mark style="color:red;">\*</mark>      | String | Expiry date of identification document (YYYY-MM-DD)                                                                                                                                                      |
| document.front<mark style="color:red;">\*</mark>             | String | <p>The front of a document file encoded <strong>in data URI base64 encoded format.</strong></p><p></p><p>The following mime types are accepted for ID documents:<br>image/jpeg,<br>image/png.</p><p></p> |
| document.back                                                | String | <p>The back of a document file encoded in data URI base64 encoded format.</p><p></p><p>The back of a document file encoded in data URI base64 encoded format</p>                                         |
| document.face                                                | String | <p>The selfie photo file encoded <strong>in data URI base64 encoded format.</strong></p><p></p><p>The following mime types are accepted for ID documents:<br>image/jpeg,<br>image/png.</p>               |
| address                                                      | Object | Delivery address                                                                                                                                                                                         |
| address.country                                              | String | Delivery country of identification document in ISO3166-1 alpha-2 format                                                                                                                                  |
| address.city                                                 | String | Delivery city                                                                                                                                                                                            |
| address.post\_code                                           | String | Delivery post code                                                                                                                                                                                       |
| address.details                                              | String | Detail delivery address                                                                                                                                                                                  |

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

<summary>Code example</summary>

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

## **Create User with KYC link**

## Create a cardholder with KYC link

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/create-with-kyc-link`

#### Request Body

| Name                                        | Type   | Description                                                                           |
| ------------------------------------------- | ------ | ------------------------------------------------------------------------------------- |
| email<mark style="color:red;">\*</mark>     | String | Email address of cardholder                                                           |
| user\_xid<mark style="color:red;">\*</mark> | String | External identifier, unique under the partner.                                        |
| user\_name                                  | String | Nickname of user account, this is a human-friendly non-unique name for a user account |

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



## **Get User KYC link**

## Get a KYC link for user

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/kyc-link`

#### Request Body

| Name                                        | Type   | Description                                              |
| ------------------------------------------- | ------ | -------------------------------------------------------- |
| user\_xid<mark style="color:red;">\*</mark> | String | External identifier, unique under the partner.           |
| level\_name                                 | String | <p>LEVEL-1 or LEVEL-2.<br>Default value is LEVEL-1. </p> |

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





## **Get User**

## Get a collection of cardholders based on provided search criteria.

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/query`

#### Request Body

| Name                                        | Type   | Description |
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

## Upload User KYC

## Upload User KYC information

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/upload-kyc`

#### Request Body

| Name                                                         | Type   | Description                                                                                                                                                                                              |
| ------------------------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| user\_xid<mark style="color:red;">\*</mark>                  | String | External identifier, unique under the partner.                                                                                                                                                           |
| individual<mark style="color:red;">\*</mark>                 | Object | Individual card holder identity information.                                                                                                                                                             |
| individual.first\_name<mark style="color:red;">\*</mark>     | String | First name of cardholder                                                                                                                                                                                 |
| individual.last\_name<mark style="color:red;">\*</mark>      | String | Last name / Surname of cardholder                                                                                                                                                                        |
| individual.date\_of\_birth<mark style="color:red;">\*</mark> | String | Date of birth (YYYY-MM-DD)                                                                                                                                                                               |
| individual.occupation                                        | String | Occupation of card holder.                                                                                                                                                                               |
| individual.annual\_income                                    | String | Annual income of card holder in card currency                                                                                                                                                            |
| document<mark style="color:red;">\*</mark>                   | Object | Government Issued Identification Document Information                                                                                                                                                    |
| document.type<mark style="color:red;">\*</mark>              | String | 1 or 2, enums in [Document Type](../../../enums/document-type.md)                                                                                                                                        |
| document.number<mark style="color:red;">\*</mark>            | String | Identification document number.                                                                                                                                                                          |
| document.country<mark style="color:red;">\*</mark>           | String | Issuing country of identification document in ISO3166-1 alpha-2 format                                                                                                                                   |
| document.expiry\_date<mark style="color:red;">\*</mark>      | String | Expiry date of identification document (YYYY-MM-DD)                                                                                                                                                      |
| document.front<mark style="color:red;">\*</mark>             | String | <p>The front of a document file encoded <strong>in data URI base64 encoded format.</strong></p><p></p><p>The following mime types are accepted for ID documents:<br>image/jpeg,<br>image/png.</p><p></p> |
| document.back                                                | String | <p>The back of a document file encoded in data URI base64 encoded format.</p><p></p><p>The back of a document file encoded in data URI base64 encoded format</p>                                         |
| address                                                      | Object | Delivery address                                                                                                                                                                                         |
| address.country                                              | String | Delivery country of identification document in ISO3166-1 alpha-2 format                                                                                                                                  |
| address.city                                                 | String | Delivery city                                                                                                                                                                                            |
| address.post\_code                                           | String | Delivery post code                                                                                                                                                                                       |
| address.details                                              | String | Detail delivery address                                                                                                                                                                                  |

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



## Change user email

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/carduser/change-email`

When updating a user’s email, if the user has a card, the associated email on the card will be updated accordingly.&#x20;

#### Request Body

| Name     | Type   | Description                     |
| -------- | ------ | ------------------------------- |
| user\_id | String | User unique ID                  |
| email    | String | New email address of cardholder |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "success": true
}
```
{% endtab %}
{% endtabs %}
