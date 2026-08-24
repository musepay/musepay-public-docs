---
description: create and query order information .
---

# Card

{% hint style="warning" %}
Every request must contain [common parameters](common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](./#demo-client)
{% endhint %}

## Apply Card

## issue a card under a specific user.

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/apply`

Only one card can be issued under a single card product.

When issuing a card, the productId must be specified and determines the card product to issue. The card product determines the card type, card face, card features, benefits, interest rates, capabilities, etc.

#### Request Body

| Name                                                | Type   | Description                                                                                                                |
| --------------------------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| user\_id<mark style="color:red;">\*</mark>          | String | The user id  is an account that holds the funds, balances, and transactions that are used to make purchases with the card. |
| request\_id<mark style="color:red;">\*</mark>       | String | External identifier for the issuing request.                                                                               |
| card\_product\_id<mark style="color:red;">\*</mark> | String | Product ID of the card to be issued                                                                                        |
| card\_level<mark style="color:red;">\*</mark>       | String | the card level of the card product to apply                                                                                |
| phone\_number<mark style="color:red;">\*</mark>     | String | <p>Mobile phone number of card holder.<br><strong>This phone number should be pre-verified by the partner.</strong></p>    |
| phone\_area\_code<mark style="color:red;">\*</mark> | String | Country _calling_ codes                                                                                                    |
| embossed\_name                                      | String | the embossed name in card face                                                                                             |

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

## Query Apply Result

## query Card Apply Result

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/apply-result`

#### Request Body

| Name                                          | Type   | Description                                  |
| --------------------------------------------- | ------ | -------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark> | String | External identifier for the issuing request. |
| apply\_id                                     | String | The apply ID of the card issuing             |
| user\_id<mark style="color:red;">\*</mark>    | String | The unique id in musewallet                  |

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

## Get Card

## get Card

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/query`

#### Request Body

| Name                                       | Type   | Description                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | The card ID of the card issued |
| user\_id<mark style="color:red;">\*</mark> | String | The unique id in musewallet    |

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

## Activate Card

## activate card

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/activate`

#### Request Body

| Name                                       | Type   | Description                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | The card ID of the card issued |
| user\_id<mark style="color:red;">\*</mark> | String | The unique id in musewallet    |

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

## Update Phone

## update phone

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/update-phone`

#### Request Body

| Name                                                | Type   | Description                    |
| --------------------------------------------------- | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark>          | String | The card ID of the card issued |
| user\_id<mark style="color:red;">\*</mark>          | String | The unique id in musewallet    |
| phone\_number<mark style="color:red;">\*</mark>     | String | New phone number for the card  |
| phone\_area\_code<mark style="color:red;">\*</mark> | String | countryCode                    |

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

## Lock Card

## lock card

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/lock`

#### Request Body

| Name                                       | Type   | Description                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | The card ID of the card issued |
| user\_id<mark style="color:red;">\*</mark> | String | The unique id in musewallet    |

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

## UnLock Card

## unlock card

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/unlock`

#### Request Body

| Name                                       | Type   | Description                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | The card ID of the card issued |
| user\_id<mark style="color:red;">\*</mark> | String | The unique id in musewallet    |

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

## Get Card Sensitive Info

## get Card sensitive info

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/card-sensitive-info`

Generate a short-lived one-time URL for retrieving sensitive information for a card. The returned URL must be consumed directly by the client facing application, through the client's IP address provided in the retrieval request.

The API Response of the callback URL will contain the following payload:

`{`&#x20;

&#x20;   `"card_id": "akflf51b3",`&#x20;

&#x20;   `"card_number": "4242424212341234",`&#x20;

&#x20;   `"expiry_month": "11",`&#x20;

&#x20;   `"expiry_year": "2028",`&#x20;

&#x20;   `"security_code": "001"`&#x20;

`}`

#### Request Body

| Name                                          | Type   | Description                    |
| --------------------------------------------- | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark>    | String | The card ID of the card issued |
| ip\_address<mark style="color:red;">\*</mark> | String | Client IP address              |
| user\_id<mark style="color:red;">\*</mark>    | String | The unique id in musewallet    |

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

## Activate Physical Card

## activate physical card

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/activate-physical`

#### Request Body

| Name                                       | Type   | Description                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | The card ID of the card issued |
| user\_id<mark style="color:red;">\*</mark> | String | The unique id in musewallet    |

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

## Change Card PIN

## get change PIN model

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/get-change-pin-model`

#### Request Body

| Name                                       | Type   | Description                    |
| ------------------------------------------ | ------ | ------------------------------ |
| card\_id<mark style="color:red;">\*</mark> | String | The card ID of the card issued |
| user\_id<mark style="color:red;">\*</mark> | String | The unique id in musewallet    |

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



## change Card PIN

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/change-pin`

#### Request Body

| Name                                        | Type   | Description                                                                 |
| ------------------------------------------- | ------ | --------------------------------------------------------------------------- |
| card\_id<mark style="color:red;">\*</mark>  | String | The card ID of the card issued                                              |
| card\_pin<mark style="color:red;">\*</mark> | String | New PIN, numeric pin, 6 digits only,  must encrypted by platform public key |
| user\_id<mark style="color:red;">\*</mark>  | String | The unique id in musewallet                                                 |

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

<summary>Code Example for Pin Encryption </summary>

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

## Replace Card

## replace Card

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/replace`

replace with a new card under same card product

#### Request Body

<table><thead><tr><th width="239">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>user_id<mark style="color:red;">*</mark></td><td>String</td><td>The unique id for card holder</td></tr><tr><td>original_card_id<mark style="color:red;">*</mark></td><td>String</td><td>The original card id</td></tr><tr><td>replace_reason<mark style="color:red;">*</mark></td><td>String</td><td>The replace reason</td></tr><tr><td>request_id<mark style="color:red;">*</mark></td><td>String</td><td>External identifier for the replace request.</td></tr></tbody></table>

**Response**

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



## Change Card Purchase Limit

## card limit

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/limitChange`

change card purchase limit

#### Request Body

<table><thead><tr><th width="239">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>user_id<mark style="color:red;">*</mark></td><td>String</td><td>The unique id for card holder</td></tr><tr><td>card_id<mark style="color:red;">*</mark></td><td>String</td><td>The card id</td></tr><tr><td>daily_purchase_limit<mark style="color:red;">*</mark></td><td>Decimal</td><td>New daily purchase limit to set</td></tr></tbody></table>

**Response**

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



## Reject Transaction

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/txn-verification-decline`

reject txn

#### Request Body

<table><thead><tr><th width="239">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>user_id<mark style="color:red;">*</mark></td><td>String</td><td>The unique id for card holder</td></tr><tr><td>request_id<mark style="color:red;">*</mark></td><td>String</td><td>External identifier for the  request.</td></tr><tr><td>card_id<mark style="color:red;">*</mark></td><td>String</td><td>The card id</td></tr><tr><td>token<mark style="color:red;">*</mark></td><td>String</td><td>OOB token to reject</td></tr></tbody></table>

**Response**

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

## Confirm Transaction

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/txn-verification-confirm`

confirm txn

#### Request Body

<table><thead><tr><th width="239">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>user_id<mark style="color:red;">*</mark></td><td>String</td><td>The unique id for card holder</td></tr><tr><td>request_id<mark style="color:red;">*</mark></td><td>String</td><td>External identifier for the  request.</td></tr><tr><td>card_id<mark style="color:red;">*</mark></td><td>String</td><td>The card id</td></tr><tr><td>token<mark style="color:red;">*</mark></td><td>String</td><td>OOB token to confirm</td></tr></tbody></table>

**Response**

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

