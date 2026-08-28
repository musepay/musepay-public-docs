# Supported Networks

{% hint style="warning" %}
Every request must contain [common parameters](../../common-parameters.md).
{% endhint %}

Returns clearing networks for a country and receiving currency.

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/networks`

## Request Body

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| country | String | Yes | Beneficiary country or region as an ISO 3166-1 alpha-2 code. |
| currency | String | Yes | Receiving currency as an ISO 4217 currency code. |

```json
{
  "country": "US",
  "currency": "USD"
}
```

## Response Body

| Name | Type | Description |
| --- | --- | --- |
| networks | Array | Supported clearing network codes. Use one as `clear_network` when creating a quote. |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "networks": ["ACH"]
  }
}
```
