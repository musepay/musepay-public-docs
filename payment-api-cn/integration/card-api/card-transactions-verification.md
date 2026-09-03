# 卡交易验证

本文介绍通过 Webhook 集成验证卡交易的流程，说明合作伙伴如何接收交易验证消息，并与客户交互以完成验证。

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### 流程概览

#### 步骤 1：触发验证

* 当交易需要验证（例如 3DS 或 OTP）时，VISA 会触发此流程。
* MuseCard 接收来自 VISA 的验证事件。

#### 步骤 2：Webhook 通知合作伙伴系统

MuseCard 向合作伙伴系统发送 Webhook 通知：

* CARD\_TX\_OOB: 带外验证（需要客户确认）。
* CARD\_TX\_OTP: 一次性密码（OTP）验证。
* CARD\_TX\_3DS\_URL: 3D Secure 验证 URL。

#### 步骤 3：客户交互

合作伙伴系统将验证消息转发给客户：

* 对于 CARD\_TX\_OTP， 客户输入 OTP 验证码。
* 对于 CARD\_TX\_3DS\_URL， 客户点击验证 URL 完成 3D Secure 流程。
* 对于 CARD\_TX\_OOB， 合作伙伴系统向客户推送消息，由客户手动确认。



### 2. CARD\_TX\_OOB 模式（带外验证）

1. 客户通过合作伙伴系统接收验证请求。
2. 客户确认或拒绝交易。
3. 合作伙伴系统通过 API 将结果发送给 MuseCard：
   * POST [/txn-verification-confirm](../../reference/api-reference/card-api/card.md#confirm-transaction) — 用于确认交易。
   * POST [/txn-verification-decline](../../reference/api-reference/card-api/card.md#reject-transaction) — 用于拒绝交易。
4. MuseCard 处理响应，并通过回调将结果发送给 VISA。

***

### 3. 重要说明

* 所有 Webhook 事件都会实时发送到合作伙伴系统。
* 合作伙伴系统负责将消息传递给客户。
* 及时处理验证响应对避免交易延迟至关重要。
