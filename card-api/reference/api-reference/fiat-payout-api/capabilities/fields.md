# Required Beneficiary Fields

{% hint style="warning" %}
Every request must contain [common parameters](../../common-parameters.md).
{% endhint %}

Returns the bank-specific beneficiary fields required for a country, currency, and bank. Send the returned keys in `beneficiaryFields` when creating a quote.

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/fields`

## Request Body

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| country | String | Yes | Beneficiary country or region as an ISO 3166-1 alpha-2 code. |
| currency | String | Yes | Receiving currency as an ISO 4217 currency code. |
| bank_code | String | Yes | MusePay platform bank code returned by the supported banks endpoint. |

```json
{
  "country": "US",
  "currency": "USD",
  "bank_code": "bank-1"
}
```

## Response Body

| Name | Type | Description |
| --- | --- | --- |
| fields | Array | Bank-specific beneficiary field definitions. |
| fields[].key | String | Case-sensitive field key to send in `beneficiaryFields`. |
| fields[].label | String | Display name for the field. |
| fields[].required | Boolean | Whether the field must be provided. |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "fields": [
      {
        "key": "routing_number",
        "label": "Routing number",
        "required": true
      }
    ]
  }
}
```
