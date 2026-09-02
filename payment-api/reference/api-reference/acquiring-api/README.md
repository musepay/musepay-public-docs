# Acquiring API

Use these endpoints to assign reusable deposit addresses, create checkout orders with per-order addresses, query transactions, submit crypto withdrawals, and verify MusePay deposit addresses.

{% hint style="info" %}
For help choosing between Wallet Mode and Checkout Mode and implementing the complete payment flow, see the [Acquiring API integration guide](../../../integration/acquiring-api/README.md).
{% endhint %}

## APIs

| API | Endpoint | Description |
| --- | --- | --- |
| [Deposit Address](wallet-mode.md#deposit-address) | `/v1/order/deposit_address` | Retrieve a fixed deposit address for an end user and crypto asset. |
| [Create Checkout Order](checkout-mode/README.md#create-checkout-order) | `/v1/order/pay` | Create a payment order and retrieve its receiving address and checkout URL. |
| [Query Order](query-order.md) | `/v1/order/query` | Retrieve a transaction and its latest status. |
| [Withdraw](wallet-mode.md#withdraw) | `/v1/order/withdraw` | Submit a crypto withdrawal transaction. |
| [Verify Deposit Address](wallet-mode.md#verifydepositaddress) | `/v1/order/verifyDepositAddress` | Check whether an address belongs to the MusePay platform. |
