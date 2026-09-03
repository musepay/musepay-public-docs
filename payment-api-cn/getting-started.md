---
description: 配置 API 访问，并完成 MusePay 集成的初始方案选择。
---

# 快速开始

MusePay API 遵循 REST 规范。接口采用面向资源的 URL，接收 JSON 请求体并返回 JSON 响应，同时使用标准 HTTP 方法和响应状态码。

## 集成清单

1. 阅读[支持的资产](integration/supported-assets.md)，确认您的产品所需的币种和网络。
2. 按照[身份验证](integration/authentication.md)指南生成 RSA 密钥对、上传公钥并为 API 请求签名。
3. 从 [API 参考](reference/api-reference/README.md)中选择需要使用的 API，并查看其请求参数和响应对象。
4. 实现相关的 [Webhook](webhook/README.md)，使您的系统能够处理异步订单和卡片事件。
5. 面向客户启用功能前，请完整测试整个流程。

{% hint style="info" %}
请将私钥保存在安全的服务端环境中，切勿在浏览器或移动应用代码中暴露私钥。
{% endhint %}

## 选择集成方案

### 收单 API

通过钱包模式为每位用户分配可重复使用的地址，或通过收银台模式为每笔订单分配临时地址，以接收数字货币付款。本指南还介绍多链收银台、指定链收银台、支付金额差异以及基于 Webhook 的对账处理。

{% content-ref url="integration/acquiring-api/" %}
[收单 API 集成](integration/acquiring-api/)
{% endcontent-ref %}

### 卡片 API

创建持卡人、发行和管理卡片、为卡账户充值，并处理卡交易验证。请先阅读集成工作流程，再通过 Card API 参考查看接口详情。

{% content-ref url="integration/card-api/" %}
[Card API 集成](integration/card-api/)
{% endcontent-ref %}

### 法币出款 API

使用 USDT 余额向第三方银行账户发送法币。集成指南将介绍如何查询支持的出款通道、创建报价、提交出款并跟踪异步状态。

{% content-ref url="integration/fiat-payout-api/" %}
[法币出款 API 集成](integration/fiat-payout-api/)
{% endcontent-ref %}
