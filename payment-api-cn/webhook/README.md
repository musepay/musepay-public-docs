# Webhook

### 配置

配置 Webhook 后，您可以接收订单状态更新通知，包括入金、出金和交易状态更新等订单事件。可在以下位置配置 Webhook URL：

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Webhook URL 配置完成后，您将开始接收订单事件通知。所有事件都会带有以下签名。&#x20;

* **sign** = Base64(_RSA_(PLATFORM\_PRIVATE\_KEY, SHA1(msgBody))

可在以下位置获取用于验证签名的公钥：

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### 数据对象

{% content-ref url="card.md" %}
[card.md](card.md)
{% endcontent-ref %}

{% content-ref url="order.md" %}
[order.md](order.md)
{% endcontent-ref %}

### 重试机制

MusePay 会向合作伙伴配置的 URL 发送 POST 请求，并期待收到 HTTP 200 响应。如果未收到响应，MusePay 将以逐步增加的间隔多次重发请求。重试将在 \[0, 2, 4, 8, 16, 32, 64] 分钟后进行。<br>
