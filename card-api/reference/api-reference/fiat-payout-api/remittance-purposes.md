# Remittance Purposes

{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md).
{% endhint %}

Returns the remittance purpose codes that can be used to create a payout. Use a code supported by the selected beneficiary bank and preserve leading zeroes.

<mark style="color:green;">`POST`</mark> `/v1/fiatpayout/payouts/remitReasons`

## Request Body

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| enterNo | String | Yes | Enterprise number issued to the organization. |

## Request Example

```json
{
  "enterNo": "E202605050001"
}
```

## Response Body

The `data` object maps each remittance purpose code to its description.

```json
{
  "code": "200",
  "message": "success",
  "data": {
    "01": "Transfer to own account",
    "02": "Family support",
    "03": "Education expenses",
    "04": "Medical expenses",
    "05": "Hotel expenses",
    "06": "Travel",
    "10": "Purchase of residential property",
    "17": "Donation",
    "30": "Salary or commission payment"
  }
}
```
