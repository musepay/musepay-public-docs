# Supported Banks

{% hint style="warning" %}
Every request must contain [common parameters](../../common-parameters.md).
{% endhint %}

Returns enabled banks or wallets for a country and receiving currency. When `amount` is provided, the result is filtered using route limits.

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/banks`

## Request Body

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| country | String | Yes | Beneficiary country or region as an ISO 3166-1 alpha-2 code. |
| currency | String | Yes | Receiving currency as an ISO 4217 currency code. |
| amount | String | No | Amount used to filter banks by supported route limits. |

```json
{
  "country": "US",
  "currency": "USD",
  "amount": "100.00"
}
```

## Response Body

| Name | Type | Description |
| --- | --- | --- |
| banks | Array | Supported bank or wallet entries. |
| banks[].bank_code | String | MusePay platform bank code. Use it as `beneficiary_bank_id` when creating a quote. |
| banks[].bank_name | String | English bank name when available; otherwise, the local bank name. |
| banks[].type | String | Institution type, such as `bank` or `wallet`. |
| banks[].clearing_networks | Array | Clearing networks available for the country and currency. |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "banks": [
      {
        "bank_code": "bank-1",
        "bank_name": "Example Bank",
        "type": "bank",
        "clearing_networks": ["ACH"]
      }
    ]
  }
}
```
