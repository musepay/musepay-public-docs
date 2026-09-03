# 卡片 API

使用这些接口可完成持卡人入驻、卡片发行与管理、卡账户充值、交易查询，以及响应交易验证请求。

{% hint style="info" %}
有关发卡和交易验证流程，请参阅 [Card API 集成指南](../../../integration/card-api/README.md)。
{% endhint %}

## API 列表

| API | 接口 | 说明 |
| --- | --- | --- |
| [创建用户](card-user.md#create-user) | `/v1/carduser/create` | 使用身份信息创建持卡人。 |
| [通过 KYC 链接创建用户](card-user.md#create-user-with-kyc-link) | `/v1/carduser/create-with-kyc-link` | 创建持卡人并获取托管 KYC 链接。 |
| [获取用户 KYC 链接](card-user.md#get-user-kyc-link) | `/v1/carduser/kyc-link` | 获取现有持卡人的 KYC 链接。 |
| [获取用户](card-user.md#get-user) | `/v1/carduser/query` | 查询持卡人信息。 |
| [上传用户 KYC](card-user.md#upload-user-kyc) | `/v1/carduser/upload-kyc` | 上传持卡人 KYC 信息。 |
| [修改用户电子邮箱](card-user.md#change-user-email) | `/v1/carduser/change-email` | 更新持卡人的电子邮箱地址。 |
| [申请卡片](card.md#apply-card) | `/v1/card/apply` | 为持卡人发行卡片。 |
| [查询申请结果](card.md#query-apply-result) | `/v1/card/apply-result` | 获取卡片申请结果。 |
| [获取卡片](card.md#get-card) | `/v1/card/query` | 获取卡片信息。 |
| [激活卡片](card.md#activate-card) | `/v1/card/activate` | 激活卡片。 |
| [更新手机号码](card.md#update-phone) | `/v1/card/update-phone` | 更新与卡片关联的手机号码。 |
| [锁定卡片](card.md#lock-card) | `/v1/card/lock` | 锁定卡片。 |
| [解锁卡片](card.md#unlock-card) | `/v1/card/unlock` | 解锁卡片。 |
| [获取卡片敏感信息](card.md#get-card-sensitive-info) | `/v1/card/card-sensitive-info` | 获取卡片敏感信息。 |
| [激活实体卡](card.md#activate-physical-card) | `/v1/card/activate-physical` | 激活实体卡。 |
| [获取修改 PIN 所需数据](card.md) | `/v1/card/get-change-pin-model` | 获取修改卡片 PIN 所需的数据。 |
| [修改卡片 PIN](card.md) | `/v1/card/change-pin` | 修改卡片 PIN。 |
| [更换卡片](card.md#replace-card) | `/v1/card/replace` | 更换现有卡片。 |
| [修改卡片消费限额](card.md#change-card-purchase-limit) | `/v1/card/limitChange` | 更新卡片消费限额。 |
| [拒绝交易](card.md#reject-transaction) | `/v1/card/txn-verification-decline` | 拒绝交易验证请求。 |
| [确认交易](card.md#confirm-transaction) | `/v1/card/txn-verification-confirm` | 确认交易验证请求。 |
| [卡片充值](card-account.md#top-up-card) | `/v1/cardaccount/topup` | 将资金转入卡账户。 |
| [查询卡账户交易](card-account.md#query-card-account-transactions) | `/v1/cardaccount/transactions` | 获取卡账户交易。 |
