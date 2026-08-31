# multiple chain checkout

## Example

{% tabs %}
{% tab title="Crypto order" %}
```bash
curl --location --request POST '/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "USDT_BSC", 
    * "amount": "150",
    * "payment_method": "on_line",   
    * "product_name": "product info",
    * "email": "payin@abcpay.io", 
      "notify_url": "https://notify.url",
      "remark": "payout test remark",
    
}'
```
{% endtab %}

{% tab title="Fiat order" %}
```bash
curl --location --request POST '/v1/order/pay' \
--header 'Content-Type: application/json' \
--data-raw '{
    * "request_id": "custom_code9982674851738108",
    * "currency": "IDR",
      "pay_currency": "USDT_BSC", 
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
    "currency":"USDT_BSC",
    "order_amount":"30",
    "status":22,
    "payment_method":"on_line",
    "receive_address":"0x050b85892F5d5ffffff516868311e7eA2043F",
    "checkout_url":"https://gateway.dev01.musepay.io/mapi/v1/open/qrCode/CnM1mFBzFDtgr0Er"
  },
  "message":"success"
}
```
