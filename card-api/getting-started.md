# Getting Started

The Card API is organized around [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer). Our API has predictable resource-oriented URLs, accepts [JSON-encoded](http://www.json.org/)  request bodies, returns [JSON-encoded](http://www.json.org/) responses, and uses standard HTTP response codes, authentication, and verbs.

\
All API uses API secret keys to authenticate requests. Any request that doesn't include an API key will return an error.

## Issuing API Credentials

Generate an API secret key for signing requests (see the next section for how to sign requests with the API secret key)::

&#x20;  \* Signature argorithm:&#x20;

```
SHA1WithRSA
```

\
&#x20; **First,** Run the following command line to generate an RSA 2048 private key (stored in muse\_secret.key):

<pre><code><strong>//generate new private key
</strong><strong>openssl req -new -newkey rsa:2048 -nodes -keyout muse_secret.key
</strong>
//export public key from private key
openssl rsa -in muse_secret.key -pubout
</code></pre>

{% hint style="info" %}
Make sure you keep the API secret key safe and secure!
{% endhint %}

**Then go to the** [**dashboard**](https://agent.musepay.io) **and upload the public key.** MuseCard will use your public key to verify the API calls.

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

**Also remember to download MuseCard's public key** as you need to verify the notification from MuseCard API.

## Signing a Request

All API calls must be authenticated.&#x20;

{% hint style="info" %}
* all the fields should be sorted in _alphabetical order_ by the _key_
* _Empty_ field should be exclude from the signature.
* fields key name are case sensitive
{% endhint %}

For example：

assume the raw data are below：

```
partner_id:200001
request_id:2022031620000900005143515921
nonce:5K8264ILTKCH16CQ2502SI8ZNMTM67VS  
```

step 1: the data should be put in the format of 'key=value' ,and sorted in _alphabetical order_ by the _key._

{% code overflow="wrap" %}
```
message="nonce=5K8264ILTKCH16CQ2502SI8ZNMTM67VS&partner_id=100001&request_id=2020031620000900005143515921"
```
{% endcode %}

step 2: attach the api signature

{% code overflow="wrap" %}
```
sign=Base64Utils.encodeToString(sign(message,privateKey))
```
{% endcode %}

<details>

<summary>Code example（JAVA）</summary>

```java
// Some code
import org.springframework.util.Base64Utils;
import java.security.KeyFactory;
import java.security.PrivateKey;
import java.security.Signature;
import java.security.spec.PKCS8EncodedKeySpec;

public static final String SIGN_ALGORITHMS = "SHA1WithRSA";

try {
    PKCS8EncodedKeySpec priPKCS8 = new PKCS8EncodedKeySpec(Base64Utils.decodeFromString(privateKey));
    KeyFactory keyf = KeyFactory.getInstance("RSA");
    PrivateKey priKey = keyf.generatePrivate(priPKCS8);
    Signature signature = Signature.getInstance(SIGN_ALGORITHMS);
    signature.initSign(priKey);
    signature.update(content.getBytes(inputCharset));
    byte[] signed = signature.sign();
    return Base64Utils.encodeToString(signed);
 } catch (Exception e) {
    e.printStackTrace();
 }
```

</details>

<details>

<summary>Code example（Javascript）</summary>

````java
```javascript
import { hex2b64, KJUR } from 'jsrsasign'
import queryString from 'query-string'
import Axios from 'axios'

function buildCommonParams() {
  return {
    partner_id: this.partnerId,
    sign_type: 'RSA',
    timestamp: new Date().getTime(),
    nonce: new Date().getTime()
  }
}

function buildSignContent(params) {
  // console.log(`privateKey: `, this.privateKey)
  Object.keys(params).forEach(key => {
    if (!params[key]) {
      params[key] = undefined
    }
  })
  params.sign = undefined
  return queryString.stringify(params, { encode: false })
}

function sign(content) {
  console.log(`sign content: `, content)
  const sig = new KJUR.crypto.Signature({ 'alg': 'SHA1withRSA', 'prov': 'cryptojs/jsrsa', 'prvkeypem': `-----BEGIN PRIVATE KEY-----${this.privateKey}-----END PRIVATE KEY-----` })
  // console.log(sig)
  sig.updateString(content)
  const signedHex = sig.sign()
  // console.log(signedHex)
  const result = hex2b64(signedHex)
  console.log(`result: `, result)
  return result
}

// example
const data = Object.assign(this.buildCommonParams(), {
  currency
})
const content = this.buildSignContent(data)
data.sign = this.sign(content)
return this.axios({
  url: '/v1/carduser/creaate',
  method: 'post',
  data: data
})
```
````

</details>

<details>

<summary>Code example（PHP）</summary>

````java
```php
<?php
// 原始数据
$data = "nonce=1694076760022&partner_id=2100063&sign_type=RSA&timestamp=1694076760022&user_id=1100133&user_xid=2";

// 私钥（从文件或字符串中获取）
//$privateKeyPem = file_get_contents("../muse_secret.key");
$privateKeyPem = "-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCnI1kB3OyurSfUaqIc7QPVbehYFeAXz3wRbr0KfL3bkF42r9lKUV5s5S3Bqfwu/L2r8kCFCVg9p6BBEZQFoGNp0LHqYThm89rWfzfFom6hncnUIUu67PYxq2tjazZRj/PxKjaGckPowXe6tbLapV2SiexdXFbW9SlsQQstXQW75aug+PElCYmy4dnv2f7OTF1PAkUTxTR1WNVhWZMRdqozmko3UsWDmT92JSYIzeES2AjktWYNAFrKGv7k/66jVHbieS9JAN6XU5EzBQ1pvlBk3oLHYRk0YKJG9Xrw822OLN8hO/Ty0et7qy/f9C38Nfw4UG4b+ZySZQJ8WbKLJMAbAgMBAAECggEAHRvk5pQpjIqPw0kHDu6gmk1YB+9XZg4213pn5imvj0vnfLLHr0/YmDKZ8369cxmFlyrL3d+wxJwrJun+07QJXGaCdgWUoymZVX42om8VwYQPoKhj3hxjDGeEfn4vqajenYPylxvTg/gd+CCpE7d1Qo5O4juwzCNKoZX6cl4fH4gqUk/yxxzFtUdA3knECmC0SxxesSqKwlKhFPfkLdvH2lBuhojfE+2Yo9AMFz4GfvDA4ds7SYPplm7K/57EA0qE75IBxuCnUIBimMFViZanmh08zbHVdlUcN1fXlxJnyv5dXh65OzLU7t96S1OXsmT3dMpRY4iJkAHdLgKLcRzSQQKBgQDdXtDqgSLV9fv5W9RABfCKlabdO+jzGwglWDQyBtTTioaTMEwY4UIxRm4YR4pXg0QNJnO6ROTcGYKrOJDD+L2WilVgVE4zntsN0Aj3vWLb7Sf/0u87nbU/HydPiSEz8H1AET60oWSXM1MLVaswynBz27QklmTINtskoF6gu3dx8QKBgQDBSLMPDLKawFSU3psRRZVQpHBQQjvkeqBHFDQzeOReQvnExuTQ3F7CE7Vw57+pvyS905sirmwUGfS+1ACqeXVz4Kn9rV2GS930oCBplJQgs7aJK0p0fALvrtL+Qjsga3FDAS8xHPzTDj66NelJI1AOFiUY/VoKwdNn40D4KR3GywKBgCvrBbOgjxK3zJe6Gi/hfclgy0wU+LBSaplOGHzcUhjt4KkO6en9tq4j9O+oMdAO4M9jE46e4HCyNvRVMpNOo/5bz3hfAWzIVVk2LrFHx3cuY8MjTAcd0LmHKrtiz02IprCxOymG43gD3LPg+Sei4hB6RBEGLVRzXaK0llF5H8dhAoGAebfFgym04/1Qhnt03bibIjCbxf8f5m9OtdREV1G/RpkY31F9UQYl6kQtE8/thAEqKxyx6nI6/6Gk3fN2A+T/ER0fD/B4IBVwzhd0sehuK/Xgcps/hQF/e971YkblIzJmHhMF3ADsOiETYYKHyZYiWOybKhSJ+pI7BoY3KNADv2cCgYAWS/XUef5V+R0xnGv6PvPWjT7q/Oa1G1RJ3uSVa3qL2WEWiwJpg+dC6wBTDsx7CRp5X0kodabLUSqCXkaho61AMwgiAgPCwGTXe4dZRs99cgNJjrer9Gcf/CYVA/43tMyuFFSvV794/oZ59nBaF3JyzeZxo3NKUgGpaKIKrlixkg==
-----END PRIVATE KEY-----";

$privateKey = openssl_pkey_get_private($privateKeyPem);

 echo "privateKeyPem: " . $privateKeyPem;
 echo "\n";

// 计算签名
$signature = "";
if (openssl_sign($data, $signature, $privateKey, OPENSSL_ALGO_SHA1)) {
    // 转换为Base64
    $base64Signature = base64_encode($signature);
    echo "Base64 Signature: " . $base64Signature;
} else {
    echo "Signing failed!";
}

// 释放私钥资源
// openssl_free_key($privateKey);
?>

```
````

</details>

step 3: finally get the request data

{% code overflow="wrap" %}
```
{     
"partner_id":"200001"     
"request_id":"2020031620000900005143515921"
"nonce":"5K8264ILTKCH16CQ2502SI8ZNMTM67VS"  
       
"sign":"LP0WrOk2N++KfizhZOoU23giqqylH1YX7U0NGm+U86Cznvf/IwvNrUVV1FZFrBOvAXBOi0EhUv2zxHzUwutww4Iuu25+qLV1L4I+kjwkE+70B0uFfoowSpCnuvHJ8fzT3uy4+KwPQCfT+H/BYEoXlSTO6VnAUD3qs9l/aQLKZxT7iURgdxVnc+7K5JiaThZ+TqFTL3kaVDD12H2orznA/QAhiosqIZXvpj4BbsvZO/c92dwS18HJKB5+qFxOwU+bsgFz6La+7ZZEnfS9cgIB43qeNi7eIVHwOH+YddbN8t+QxNDCZAaAf6p9mX8OhsuBi93cJZwh52jqmoFluOJbww=="
}

```
{% endcode %}

## IP Whitelisting

\
MuseCard supports restriction of API calls to be accepted only from a specific IP address per API key. If you wish to whitelist your IP address, please contact our technical support with the IP of the machine running your API client and the matching API key.

<br>

