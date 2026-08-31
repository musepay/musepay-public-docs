# WebHook

### Setting up

Setting a web-hook will allow you to get notifications for order status update. You can receive notifications on events in your orders such as incoming/outgoing transactions and transactions status update.  The Webhook url can be set up here:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Once your webHook url is setup, you will start receiving notification on events for your orders. All events will be sent with the following signature.&#x20;

* **sign** = Base64(_RSA_(PLATFORM\_PRIVATE\_KEY, SHA1(msgBody))

The public key for verifying the signature can be found here:

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Data Objects

{% content-ref url="card.md" %}
[card.md](card.md)
{% endcontent-ref %}

{% content-ref url="order.md" %}
[order.md](order.md)
{% endcontent-ref %}

### Retry attempts

MusePay will send a POST request to the URL(s) associated with the partner and expect a 200 response. If no response is received, MusePay will resend the request several more times with an increasing delay between each attempt, the retry attemps will be taken after \[ 0,2,4,8,16,32,64] minutes.<br>
