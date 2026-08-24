---
description: API endpoints pertaining to the shared-quota.
---

# Shared Quota

{% hint style="warning" %}
Every request must contain [common parameters](common-parameters.md)
{% endhint %}

{% hint style="info" %}
Demo code can be found at [Github](./#demo-client)
{% endhint %}



### **Shared Quota**

Multiple Shared Quota Cards can be issued under a single Budget Quota, allowing all cards to share the same budget balance.

Shared Quota Cards only define individual spending limits for each card; they do not carry actual funds themselves. All fees, transactions, and refunds are directly settled against the Budget Quota balance.

Funds transfer into or out from the Budget Quota are directly linked to the Main Account balance.

> **Note:** \
> If the total spending limits assigned to all Shared Quota Cards exceed the available Budget Quota balance, an over-limit fee may apply based on the excess amount.

### **Over-limit Fee Explanation**

Each Budget Quota represents the actual funds deposited by the merchant. However, you may assign card limits exceeding the total Budget Quota.

If the total card limits exceed the actual Budget Quota balance, the excess amount will be considered as an over-limit allocation and **will incur a management fee on the exceeding portion.**

**Fee Calculation Example:**

**Example 1:**

Merchant funds 50,000 USDT into the Budget Quota and there are 10 cards under this budget quota.

They assign limits of 10,000 USDT to each of 10 cards (total assigned limits = 100,000 USDT).

Over-limit amount = 100,000 USDT - 50,000 USDT = 50,000 USDT.

Management fee will apply to the 50,000 USDT over-limit amount and will be charged in daily basis.

**Example 2:**

Merchant funds 30,000 USDT into the Budget Quota.

Limits assigned to 5 cards:

* Card 1: 10,000 USDT
* Card 2: 10,000 USDT
* Card 3: 10,000 USDT
*   Card 4 & Card 5: 0 USDT

    Total assigned limits = 30,000 USDT → No over-limit fee (limits match the budget).

### Integration Flow

> Create Budget Quota → Fund Budget Quota → Apply for Shared Quota Cards

[**Step 1: Create a Budget Quota**](shared-quota.md#create-a-budget-quota)

Initiate the creation of a Budget Quota. This serves as the shared fund pool that will be used by all linked Shared Quota Cards.

[**Step 2: Fund the Budget Quota** ](shared-quota.md#fund-the-budget-quota)

Deposit funds into the Budget Quota. The deposited amount will become the available balance for all associated Shared Quota Cards.

[**Step 3: Apply for Shared Quota Cards**](shared-quota.md#apply-for-shared-quota-cards)

Once the Budget Quota is funded, you can issue Shared Quota Cards under this quota.

Each card’s spending limit can be adjusted through the [Top-up API](card-account.md#top-up-card). This top-up action does not deduct from the Budget Quota balance; it only defines the card’s spending limit.



## Create a b**udget** quota

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/quota/create`

#### Request Body

| Name                                                 | Type   | Description                                 |
| ---------------------------------------------------- | ------ | ------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark>        | String | External identifier for the create request. |
| card\_product\_id<mark style="color:red;">\*</mark>  | String | Product ID of the card to be related        |
| card\_level<mark style="color:red;">\*</mark>        | String | the card level of the card product          |
| share\_quota\_name<mark style="color:red;">\*</mark> | String | the name of the budget quota                |
| remark                                               | String | remark                                      |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    // Response
   "code":200,
   "message":"success",
   "data": {
        "share_quota_id": "2469990273197955",
        "share_quota_status": "NORMAL"
    }
}
```
{% endtab %}
{% endtabs %}

## **Fund the Budget Quota**&#x20;

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/quota/tx/adjustment`

#### Request Body

| Name                                               | Type    | Description                          |
| -------------------------------------------------- | ------- | ------------------------------------ |
| share\_quota\_id<mark style="color:red;">\*</mark> | String  | the budget quota id                  |
| request\_id<mark style="color:red;">\*</mark>      | String  | External identifier for the request. |
| amount<mark style="color:red;">\*</mark>           | Integer | the amount to set                    |
| remark                                             | String  | remark                               |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    // Response
   "code":200,
   "message":"success",
   "data": {
        "status": "APPLYING",
        "order_no": "2469990273197955",
        "amount": "120",
        "request_id": "afdsfasf234324"
    }
}
```
{% endtab %}
{% endtabs %}



## **Apply for Shared Quota Cards**&#x20;

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/apply`

#### Request Body

| Name                                                | Type   | Description                                                                                                                |
| --------------------------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| user\_id<mark style="color:red;">\*</mark>          | String | The user id  is an account that holds the funds, balances, and transactions that are used to make purchases with the card. |
| request\_id<mark style="color:red;">\*</mark>       | String | External identifier for the issuing request.                                                                               |
| card\_product\_id<mark style="color:red;">\*</mark> | String | Product ID of the card to be issued                                                                                        |
| card\_level<mark style="color:red;">\*</mark>       | String | the card level of the card product to apply                                                                                |
| phone\_number<mark style="color:red;">\*</mark>     | String | <p>Mobile phone number of card holder.<br><strong>This phone number should be pre-verified by the partner.</strong></p>    |
| phone\_area\_code<mark style="color:red;">\*</mark> | String | Country _calling_ codes                                                                                                    |
| embossed\_name                                      | String | the embossed name in card face                                                                                             |
| share\_quota\_id<mark style="color:red;">\*</mark>  | String | the budget quota id                                                                                                        |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
    // Response
   "code":200,
   "message":"success",
   "data": {
        "apply_status": "APPLYING",
        "apply_id": "2469990273197955",
        "request_id": "afdsfasf234324"
    }
}
```
{% endtab %}
{% endtabs %}



## Query b**udget** quota records

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/quota/list`

#### Request Body

| Name             | Type   | Description                               |
| ---------------- | ------ | ----------------------------------------- |
| share\_quota\_id | String | the budget quota id (optional)            |
| limit            | String | page size, default 10, between 1 and 1000 |
| page             | int    | page number, default 1                    |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
  "code": "200",
  "data": {
    "total": 100,
    "data": [
      {
        "share_quota_id": "TD13614342296065",
        "share_quota_name": "aaaaa",
        "card_product_id": "2daca29b5ed4e28a92dca87",
        "card_level": 1,
        "share_quota_status": "xx",
        "share_quota_currency": "USDT",
        "available_quota_balance":12321,
        "outgoing_quota_balance": 1696861482753,
        "total_usage_quota_balance": 1696861482753,
        "available_card_tx_quota": 1696861482753,
        "total_card_tx_quota": 1696861482753,
        "total_issue_card_count": 10
      },
    ]
  },
  "message": "success"
}
```
{% endtab %}
{% endtabs %}



## Query Budget Quota Adjustment History

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/quota/tx/list`&#x20;

#### Request Body

| Name             | Type   | Description                                                       |
| ---------------- | ------ | ----------------------------------------------------------------- |
| share\_quota\_id | String | the budget quota id (optional)                                    |
| request\_id      | String | External identifier for the adjust request.                       |
| start\_time      | Long   | Start time in milliseconds (Unix timestamp), e.g., 1748188799000L |
| end\_time        | Long   | End time in milliseconds (Unix timestamp), e.g., 1748188799000L   |
| limit            | String | page size, default 10, between 1 and 1000                         |
| page             | int    | page number, default 1                                            |

{% tabs %}
{% tab title="200: OK Success" %}
```json
{
  "code": "200",
  "data": {
    "total": 100,
    "data": [
      {
        "share_quota_id": "TD13614342296065",
        "order_no": "aaaaa",
        "status": "dsf",
        "request_id": "2daca29b5ed4e28a92dca87",
        "amount":12321,
        "transaction_time": 1748188799000
      },
    ]
  },
  "message": "success"
}
```
{% endtab %}
{% endtabs %}
