# 多链收银台

使用 `payment_method=on_line` 并将资产代码设为通用的 `USDT`。托管收银台页面会允许用户选择任何受支持的 USDT 网络。

## 示例

{% tabs %}
{% tab title="数字货币订单" %}
```bash
curl --location --request POST '/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "USDT",
    * "amount": "150",
    * "payment_method": "on_line",   
    * "product_name": "product info",
    * "email": "payin@abcpay.io", 
      "notify_url": "https://notify.url",
      "remark": "payout test remark",
    
}'
```
{% endtab %}

{% tab title="法币订单" %}
```bash
curl --location --request POST '/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "IDR",
      "pay_currency": "USDT",
    * "amount": "21000",  //fiat amount
    * "payment_method": "on_line",   
    * "product_name": "product info",
      "customer_ref_id": "abc123",
    * "notify_url": "https://notify.url"
    
}'
```
{% endtab %}
{% endtabs %}

```json
// response
{
  "code":"200",
  "data": {
    "request_id":"custom_code9982674851738108",
    "partner_id":"2000051",
    "order_no":"202406173100230009031352048",
    "currency":"USDT",
    "order_amount":"30",
    "status":22,
    "payment_method":"on_line",
    "receive_address":"0x050b85892F5d5ffffff516868311e7eA2043F",
    "checkout_url":"https://gateway.dev01.musepay.io/mapi/v1/open/qrCode/CnM1mFBzFDtgr0Er"
  },
  "message":"success"
}
```
