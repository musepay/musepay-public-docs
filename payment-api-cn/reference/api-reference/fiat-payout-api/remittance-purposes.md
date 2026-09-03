# 汇款用途

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md).
{% endhint %}

返回可用于创建出款的汇款用途代码。请使用所选收款银行支持的代码，并保留前导零。

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/payouts/remitReasons`

## 响应 Body

`data` 对象将每个汇款用途代码映射到对应说明。

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "01": "Transfer to own account",
    "02": "Family support",
    "03": "Education-related student expenses",
    "04": "Medical expenses",
    "05": "Hotel expenses",
    "06": "Travel",
    "07": "Utility bill payments",
    "08": "Loan repayment",
    "09": "Tax payment",
    "10": "Purchase of residential property",
    "11": "Rent payment",
    "12": "Insurance prepayment",
    "13": "Product insurance",
    "14": "Insurance premium payment",
    "15": "Mutual fund investment",
    "16": "Equity investment",
    "17": "Donation",
    "18": "Information service fees",
    "19": "Advertising or public relations expenses",
    "20": "Loyalty service fees, trademark fees, patent fees, and copyright fees",
    "21": "Transaction, guarantee, and factoring fees",
    "22": "Consulting, technical service, academic, and expert fees",
    "23": "Representative office expenses",
    "24": "Building construction costs",
    "25": "Goods transfer fees",
    "26": "Payment for exported goods",
    "27": "Goods logistics fees",
    "28": "General offline trade in goods",
    "29": "Other trade-in-services expenses",
    "30": "Salary or commission payment",
    "31": "Regular maintenance fees",
    "32": "Computer service fees",
    "33": "Small-value remittance",
    "34": "Liberalized remittance",
    "35": "Bonus payment",
    "36": "Influencer fees"
  }
}
```
