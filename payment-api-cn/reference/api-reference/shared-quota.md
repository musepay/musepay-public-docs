---
description: 与共享额度相关的 API 接口。
hidden: true
---

# 共享额度

{% hint style="warning" %}
每个请求都必须包含[通用参数](common-parameters.md)
{% endhint %}

{% hint style="info" %}
示例代码位于 [Github](./#demo-client)
{% endhint %}



### **共享额度**

一个预算额度下可发行多张共享额度卡，所有卡片共享同一预算余额。

共享额度卡仅为每张卡定义独立消费限额，卡片本身不承载实际资金。所有费用、交易和退款都直接从预算额度余额中结算。

转入或转出预算额度的资金与主账户余额直接关联。

> **注意：** \
> 如果分配给所有共享额度卡的消费限额总和超过可用预算额度余额，可能会根据超出金额收取超额费用。

### **超额费用说明**

每个预算额度代表商户实际存入的资金。但您可以分配超过预算额度总额的卡片限额。

如果卡片限额总和超过实际预算额度余额，超出部分将被视为超额分配，并**对超出部分收取管理费**。

**费用计算示例：**

**示例 1：**

商户向预算额度充入 50,000 USDT，该预算额度下有 10 张卡。

商户为 10 张卡每张分配 10,000 USDT 限额（已分配限额总和 = 100,000 USDT）。

超额金额 = 100,000 USDT - 50,000 USDT = 50,000 USDT。

将对 50,000 USDT 的超额金额按日收取管理费。

**示例 2：**

商户向预算额度充入 30,000 USDT。

为 5 张卡分配的限额：

* 卡片 1：10,000 USDT
* 卡片 2：10,000 USDT
* 卡片 3：10,000 USDT
*   卡片 4 和卡片 5：0 USDT

    已分配限额总和 = 30,000 USDT → 不收取超额费用（限额与预算匹配）。

### 集成流程

> 创建预算额度 → 为预算额度充值 → 申请共享额度卡

[**步骤 1：创建预算额度**](shared-quota.md#create-a-budget-quota)

发起创建预算额度。该额度将作为所有关联共享额度卡使用的共享资金池。

[**步骤 2：为预算额度充值** ](shared-quota.md#fund-the-budget-quota)

将资金存入预算额度。存入金额将成为所有关联共享额度卡的可用余额。

[**步骤 3：申请共享额度卡**](shared-quota.md#apply-for-shared-quota-cards)

预算额度充值后，即可在该额度下发行共享额度卡。

可通过[充值 API](card-api/card-account.md#top-up-card)调整每张卡的消费限额。此充值操作不会从预算额度余额中扣款，仅用于定义卡片的消费限额。



## 创建预算额度

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/quota/create`

#### 请求 Body

| 名称                                                 | 类型   | 说明                                 |
| ---------------------------------------------------- | ------ | ------------------------------------------- |
| request\_id<mark style="color:red;">\*</mark>        | String | 创建请求的外部标识符。 |
| card\_product\_id<mark style="color:red;">\*</mark>  | String | 要关联的卡片产品 ID        |
| card\_level<mark style="color:red;">\*</mark>        | String | 卡片产品的卡片等级          |
| share\_quota\_name<mark style="color:red;">\*</mark> | String | 预算额度名称                |
| remark                                               | String | 备注                                      |

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

## **为预算额度充值**&#x20;

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/quota/tx/adjustment`

#### 请求 Body

| 名称                                               | 类型    | 说明                          |
| -------------------------------------------------- | ------- | ------------------------------------ |
| share\_quota\_id<mark style="color:red;">\*</mark> | String  | 预算额度 ID                  |
| request\_id<mark style="color:red;">\*</mark>      | String  | 请求的外部标识符。 |
| amount<mark style="color:red;">\*</mark>           | Integer | 要设置的金额                    |
| remark                                             | String  | 备注                               |

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



## **申请共享额度卡**&#x20;

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/apply`

#### 请求 Body

| 名称                                                | 类型   | 说明                                                                                                                |
| --------------------------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| user\_id<mark style="color:red;">\*</mark>          | String | 用户 ID 对应一个账户，用于保存卡片消费所需的资金、余额和交易。 |
| request\_id<mark style="color:red;">\*</mark>       | String | 发卡请求的外部标识符。                                                                               |
| card\_product\_id<mark style="color:red;">\*</mark> | String | 要发行的卡片产品 ID                                                                                        |
| card\_level<mark style="color:red;">\*</mark>       | String | 要申请的卡产品等级                                                                                |
| phone\_number<mark style="color:red;">\*</mark>     | String | <p>持卡人手机号码。<br><strong>该手机号码应由合作伙伴预先验证。</strong></p>    |
| phone\_area\_code<mark style="color:red;">\*</mark> | String | 国家/地区电话区号                                                                                                    |
| embossed\_name                                      | String | 卡面上的压印姓名                                                                                             |
| share\_quota\_id<mark style="color:red;">\*</mark>  | String | 预算额度 ID                                                                                                        |

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



## 查询预算额度记录

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/quota/list`

#### 请求 Body

| 名称             | 类型   | 说明                               |
| ---------------- | ------ | ----------------------------------------- |
| share\_quota\_id | String | 预算额度 ID（可选）            |
| limit            | String | 每页数量，默认为 10，取值范围为 1–1000 |
| page             | int    | 页码，默认为 1                    |

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



## 查询预算额度调整记录

<mark style="color:green;">`POST`</mark> `https://api.musepay.io/v1/card/share-quota/quota/tx/list`&#x20;

#### 请求 Body

| 名称             | 类型   | 说明                                                       |
| ---------------- | ------ | ----------------------------------------------------------------- |
| share\_quota\_id | String | 预算额度 ID（可选）                                    |
| request\_id      | String | 额度调整请求的外部标识符。                       |
| start\_time      | Long   | 开始时间，为 Unix 毫秒时间戳，例如 1748188799000L |
| end\_time        | Long   | 结束时间，为 Unix 毫秒时间戳，例如 1748188799000L   |
| limit            | String | 每页数量，默认为 10，取值范围为 1–1000                         |
| page             | int    | 页码，默认为 1                                            |

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
