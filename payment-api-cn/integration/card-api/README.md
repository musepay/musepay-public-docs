---
description: 集成持卡人入驻、发卡、充值、管理和交易验证。
---

# 卡片 API

MusePay Card API 帮助合作伙伴在自己的产品中构建完整的卡片体验。您可以创建和管理持卡人、发行卡片、管理卡片状态和设置、为卡账户充值，以及响应交易验证请求。

## 集成流程

{% content-ref url="how-to-issue-a-card.md" %}
[如何发行卡片](how-to-issue-a-card.md)
{% endcontent-ref %}

{% content-ref url="card-transactions-verification.md" %}
[卡交易验证](card-transactions-verification.md)
{% endcontent-ref %}

## API 参考

实现上述流程时，请参考以下接口文档：

* [卡用户](../../reference/api-reference/card-api/card-user.md) — 创建持卡人并管理身份与 KYC 信息。
* [卡片](../../reference/api-reference/card-api/card.md) — 发卡、查询、激活、锁定、更新或换卡，并响应验证请求。
* [卡账户](../../reference/api-reference/card-api/card-account.md) — 为卡片充值并查询卡账户交易。
