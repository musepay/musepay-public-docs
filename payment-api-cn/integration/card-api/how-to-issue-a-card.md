# 如何发行卡片

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

### 1. 获取卡产品 ID

发卡时必须指定 `productId`，它决定要发行的卡产品。卡产品决定卡类型、卡面、卡功能、权益、利率和支持的能力等。可用的 `productId` 列表是固定的，由您的解决方案经理提供。您也可以从 Partner Portal（[https://partner.musepay.io/](https://partner.musepay.io/)）查询 `productId`。

### 2. 创建持卡人

按照[身份验证](../authentication.md)指南配置 API 访问，然后使用[卡用户](../../reference/api-reference/card-api/card-user.md)接口创建持卡人。

### 3. 申请卡片

创建持卡人后，使用[申请卡片](../../reference/api-reference/card-api/card.md#apply-card)接口提交卡片申请。

### 4. 充值

* 首先，您需要向 partner basic account 充入一定数量的数字货币资产。前往 Partner Portal，然后进入 **Balance → Deposit Coin**，即可获取数字货币地址。数字货币在链上确认后，您的 partner basic account 将获得余额。

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

*   然后使用[卡片充值](../../reference/api-reference/card-api/card-account.md#top-up-card)接口。MusePay 会将指定金额从您的 partner basic account 转入选定的卡账户。

    <br>
