# 收单 API

使用这些接口可为用户分配可重复使用的充值地址、创建按订单分配地址的收银台订单、查询交易、提交数字货币提现，以及验证 MusePay 充值地址。

{% hint style="info" %}
如需选择 Wallet Mode 或 Checkout Mode 并实现完整支付流程，请参阅[收单 API 集成指南](../../../integration/acquiring-api/README.md)。
{% endhint %}

## API 列表

| API | 接口 | 说明 |
| --- | --- | --- |
| [充值地址](wallet-mode.md#deposit-address) | `/v1/order/deposit_address` | 获取某个最终用户和数字货币资产的固定充值地址。 |
| [创建收银台订单](checkout-mode/README.md#create-checkout-order) | `/v1/order/pay` | 创建支付订单，并获取收款地址和收银台 URL。 |
| [查询订单](query-order.md) | `/v1/order/query` | 获取交易及其最新状态。 |
| [提现](wallet-mode.md#withdraw) | `/v1/order/withdraw` | 提交数字货币提现交易。 |
| [验证充值地址](wallet-mode.md#verifydepositaddress) | `/v1/order/verifyDepositAddress` | 检查地址是否属于 MusePay 平台。 |
