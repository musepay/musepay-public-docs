---
description: 获取卡账户信息
---

# 卡账户

{% hint style="warning" %}
每个请求都必须包含[通用参数](../common-parameters.md)
{% endhint %}

{% hint style="info" %}
示例代码位于 [Github](../#demo-client)
{% endhint %}



## 卡片充值

## 为卡片充值

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/cardaccount/topup`

#### 请求 Body

| 名称                                          | 类型   | 说明                                 |
| --------------------------------------------- | ------ | ------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark> | String | 充值请求的外部标识符。 |
| card\_id<mark style="color:red;">\*</mark>    | String | 已发行卡片的卡片 ID              |
| amount<mark style="color:red;">\*</mark>      | String | 充值金额                            |
| currency<mark style="color:red;">\*</mark>    | String | 扣款币种               |
| user\_id<mark style="color:red;">\*</mark>    | String | MuseWallet 中的用户唯一 ID            |

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



## **查询卡账户交易**

## 查询卡账户交易

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/cardaccount/transactions`

#### 请求 Body

| 名称                                       | 类型   | 说明                                 |
| ------------------------------------------ | ------ | ------------------------------------------- |
| card\_id<mark style="color:red;">\*</mark> | String | 已发行卡片的卡片 ID              |
| order\_no                                  | String | 交易订单 ID                        |
| date\_range\_from                          | Number |                                             |
| date\_range\_to                            | Number |                                             |
| page\_size                                 | Number | 默认为 50，取值范围为 1–1000              |
| user\_id<mark style="color:red;">\*</mark> | String | MuseWallet 中的用户唯一 ID            |
| request\_id                                | String | 充值请求的外部标识符。 |
| page\_number                               | Number | 默认为 1                                   |
| tx\_status                                 | String | 交易状态                                   |
| tx\_type                                   | String | 交易类型                                     |
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

