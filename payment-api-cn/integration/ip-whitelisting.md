---
description: 将 API 访问限制为已批准的服务器 IP 地址。
---

# IP 白名单

MusePay 可以对使用某个 API Key 发起的请求进行限制，仅接受来自已批准 IP 地址的请求。

如需配置 IP 白名单，请联系 MusePay 技术支持并提供：

* 需要配置的 API Key 标识。
* 每台调用 MusePay API 的服务器的公网出口 IP 地址。

{% hint style="warning" %}
切勿将私钥发送给 MusePay 或任何第三方。MusePay 配置白名单时只需要 API Key 标识和 IP 地址。
{% endhint %}

请使用稳定的出口 IP 地址。来自白名单以外地址的请求将不会被接受。
