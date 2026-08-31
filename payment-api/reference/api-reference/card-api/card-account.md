---
description: Retrieve information of card accounts
---

# Card Account

{% hint style="warning" %}
Every request must contain [common parameters](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](../#demo-client)
{% endhint %}



## Top Up Card

## top up card

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/cardaccount/topup`

#### Request Body

| Name                                          | Type   | Description                                 |
| --------------------------------------------- | ------ | ------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark> | String | External identifier for the top up request. |
| card\_id<mark style="color:red;">\*</mark>    | String | The card ID of the card issued              |
| amount<mark style="color:red;">\*</mark>      | String | Amount to top up                            |
| currency<mark style="color:red;">\*</mark>    | String | Currency for amount deduction               |
| user\_id<mark style="color:red;">\*</mark>    | String | The unique user id in MuseWallet            |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript
{
  "code": "200",
  "data": {
    "amount": "5.880000000000000000",
    "currency": "USDT_TRC20",
    "fee": "0",
    "order_no": "2023169681108404690947",
    "request_id": "e6dcba5ced67d59",
    "status": "PENDING"
  },
  "message": "success"
}


```
{% endtab %}
{% endtabs %}



## **Query Card Account Transactions**

## query card account transactions

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/cardaccount/transactions`

#### Request Body

| Name                                       | Type   | Description                                 |
| ------------------------------------------ | ------ | ------------------------------------------- |
| card\_id<mark style="color:red;">\*</mark> | String | The card ID of the card issued              |
| order\_no                                  | String | transaction order id                        |
| date\_range\_from                          | Number |                                             |
| date\_range\_to                            | Number |                                             |
| page\_size                                 | Number | default 50, between 1 and 1000              |
| user\_id<mark style="color:red;">\*</mark> | String | The unique user id in MuseWallet            |
| request\_id                                | String | External identifier for the top up request. |
| page\_number                               | Number | default 1                                   |
| tx\_status                                 | String | tx status                                   |
| tx\_type                                   | String | tx type                                     |
| detail\_id                                 | String |                                             |

{% tabs %}
{% tab title="200: OK Success" %}
```javascript

{
  "code": "200",
  "data": {
    "card_id": "VC130798262733",
    "page_number": 1,
    "page_size": 50,
    "total_count": 1,
    "transactions": [
      {
        "detailId": "TD13614342296065",
        "order": {
          "fee": 0,
          "feeCurrency": "USDT_TRC20",
          "orderAmount": 5.880000000000000000,
          "orderCurrency": "USDT",
          "orderNo": "202316968614802662142296064",
          "paymentAmount": 5.880000000000000000,
          "paymentCurrency": "USDT_TRC20",
          "rate": 1,
          "status": "SUCCESS"
        },
        "orderNo": "202316968614802302296064",
        "requestId": "2daca29b5ed4e28a92dca87",
        "txAmount": 5.880000000000000000,
        "txCreatedAt": 1696861480230,
        "txCurrency": "USDT",
        "txPostedAt": 1696861482753,
        "txStatus": "POSTED",
        "txType": "TOP_UP"
      },
      {
        "authorization": {
          "amount": 8862.81,
          "currency": "THB"
        },
        "detailId": "TD1362376942444550",
        "merchant": {
          "category": "Eating places and Restaurants",
          "country": "TH",
          "mcc": "5812",
          "name": "GINZADO (THAILAND)-SUK BANGKOK THA"
        },
        "txAmount": 250.220000000000000000,
        "txCreatedAt": 1696860705880,
        "txCurrency": "USDT",
        "txPostedAt": 0,
        "txStatus": "PENDING",
        "txType": "CHARGE"
      },
      {
        "detailId": "TD136452797095946",
        "order": {
          "fee": 0,
          "feeCurrency": "USDT_TRC20",
          "orderAmount": 5.880000000000000000,
          "orderCurrency": "USDT",
          "orderNo": "202316996491361410452797095945",
          "paymentAmount": 5.880000000000000000,
          "paymentCurrency": "USDT_TRC20",
          "rate": 1,
          "status": "SUCCESS"
        },
        "orderNo": "2023166596491361410452797095945",
        "requestId": "163490ae978202cf67945121f0",
        "txAmount": 5.880000000000000000,
        "txCreatedAt": 1696860659649,
        "txCurrency": "USDT",
        "txPostedAt": 1696860663335,
        "txStatus": "POSTED",
        "txType": "TOP_UP"
      }
    ],
    "user_id": 60004408
  },
  "message": "success"
}

```
{% endtab %}
{% endtabs %}

