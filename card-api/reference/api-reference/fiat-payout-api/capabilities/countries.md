# Supported Countries

{% hint style="warning" %}
Every request must contain [common parameters](../../common-parameters.md).
{% endhint %}

Returns supported beneficiary countries and the fiat currencies available in each country.

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/supports/countries`

## Request Body

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| receive_currency | String | No | Limits results to a specific receiving currency. Omit it to return all supported country and currency combinations. |

```json
{
  "receive_currency": "USD"
}
```

## Response Body

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
