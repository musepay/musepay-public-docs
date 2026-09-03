# 法币出款 API

使用这些接口可查询支持的出款通道、创建报价、从 USDT 余额提交法币出款，并查询其状态。

{% hint style="info" %}
有关建议的实现顺序和运营要求，请参阅[法币出款 API 集成指南](../../../integration/fiat-payout-api/README.md)。
{% endhint %}

## API 列表

| API | 接口 | 说明 |
| --- | --- | --- |
| [出款报价](quotations.md) | `/v1/fiatpayout/payouts/quote` | 创建出款报价并记录收款人详情。 |
| [创建法币出款](create-payout.md) | `/v1/fiatpayout/payouts/create` | 确认有效报价并开始处理出款。 |
| [查询法币出款](query-payout.md) | `/v1/fiatpayout/payouts/query` | 获取出款及其最新状态。 |
| [汇款用途](remittance-purposes.md) | `/v1/fiatpayout/payouts/remitReasons` | 获取可用的汇款用途代码。 |
| [支持的国家/地区](./capabilities/countries.md) | `/v1/fiatpayout/supports/countries` | 获取支持的国家/地区和币种。 |
| [支持的银行](./capabilities/banks.md) | `/v1/fiatpayout/supports/banks` | 获取某出款通道支持的银行或钱包。 |
| [支持的清算网络](./capabilities/networks.md) | `/v1/fiatpayout/supports/networks` | 获取某出款通道支持的清算网络。 |
| [必需的收款人字段](./capabilities/fields.md) | `/v1/fiatpayout/supports/fields` | 获取银行特定的收款人字段。 |
