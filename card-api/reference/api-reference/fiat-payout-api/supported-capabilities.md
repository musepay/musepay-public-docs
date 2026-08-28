# Supported Payout Capabilities

{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md).
{% endhint %}

Use these endpoints before creating a quote. Available banks, clearing networks, and beneficiary fields can vary by country and currency. The optional bank-query amount can also affect which banks are available.

## Supported Countries

Returns supported beneficiary countries and the fiat currencies available in each country.

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/countries`

### Request Body

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| receive_currency | String | No | Limits results to a specific receiving currency. Omit it to return all supported country and currency combinations. |

```json
{
  "receive_currency": "USD"
}
```

### Response Body

| Name | Type | Description |
| --- | --- | --- |
| countries | Array | Supported country entries, sorted by country code. |
| countries[].country | String | Country or region as an ISO 3166-1 alpha-2 code. |
| countries[].currencies | Array | Supported receiving currencies for the country. |

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "countries": [
      {
        "country": "US",
        "currencies": ["USD"]
      }
    ]
  }
}
```

## Supported Banks

Returns enabled banks or wallets for a country and receiving currency. When `amount` is provided, the result is filtered using route limits.

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/banks`

### Request Body

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

### Response Body

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

## Supported Networks

Returns clearing networks for a country and receiving currency.

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/networks`

### Request Body

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

### Response Body

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

## Required Beneficiary Fields

Returns the bank-specific beneficiary fields required for a country, currency, and bank. Send the returned keys in `beneficiaryFields` when creating a quote.

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/fields`

### Request Body

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

### Response Body

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
