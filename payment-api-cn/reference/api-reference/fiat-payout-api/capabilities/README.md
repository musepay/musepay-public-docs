# 能力查询

创建出款报价前，请先使用这些接口。可用银行、清算网络和收款人字段可能因国家/地区和币种而异。银行查询中可选的金额参数也可能影响可用银行。

| API | 接口 | 说明 |
| --- | --- | --- |
| [支持的国家/地区](./countries.md) | `/v1/fiatpayout/supports/countries` | 获取支持的国家/地区和币种。 |
| [支持的银行](./banks.md) | `/v1/fiatpayout/supports/banks` | 获取某出款通道支持的银行或钱包。 |
| [支持的清算网络](./networks.md) | `/v1/fiatpayout/supports/networks` | 获取某出款通道支持的清算网络。 |
| [必需的收款人字段](./fields.md) | `/v1/fiatpayout/supports/fields` | 获取银行特定的收款人字段。 |
