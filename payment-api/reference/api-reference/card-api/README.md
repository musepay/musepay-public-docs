# Card API

Use these endpoints to onboard cardholders, issue and manage cards, fund card accounts, query transactions, and respond to transaction verification requests.

{% hint style="info" %}
For card issuance and transaction verification workflows, see the [Card API integration guide](../../../integration/card-api/README.md).
{% endhint %}

## APIs

| API | Endpoint | Description |
| --- | --- | --- |
| [Create User](card-user.md#create-user) | `/v1/carduser/create` | Create a cardholder with identity information. |
| [Create User with KYC Link](card-user.md#create-user-with-kyc-link) | `/v1/carduser/create-with-kyc-link` | Create a cardholder and retrieve a hosted KYC link. |
| [Get User KYC Link](card-user.md#get-user-kyc-link) | `/v1/carduser/kyc-link` | Retrieve a KYC link for an existing cardholder. |
| [Get User](card-user.md#get-user) | `/v1/carduser/query` | Query cardholder information. |
| [Upload User KYC](card-user.md#upload-user-kyc) | `/v1/carduser/upload-kyc` | Upload cardholder KYC information. |
| [Change User Email](card-user.md#change-user-email) | `/v1/carduser/change-email` | Update a cardholder's email address. |
| [Apply Card](card.md#apply-card) | `/v1/card/apply` | Issue a card for a cardholder. |
| [Query Apply Result](card.md#query-apply-result) | `/v1/card/apply-result` | Retrieve the result of a card application. |
| [Get Card](card.md#get-card) | `/v1/card/query` | Retrieve card information. |
| [Activate Card](card.md#activate-card) | `/v1/card/activate` | Activate a card. |
| [Update Phone](card.md#update-phone) | `/v1/card/update-phone` | Update the phone number associated with a card. |
| [Lock Card](card.md#lock-card) | `/v1/card/lock` | Lock a card. |
| [Unlock Card](card.md#unlock-card) | `/v1/card/unlock` | Unlock a card. |
| [Get Card Sensitive Info](card.md#get-card-sensitive-info) | `/v1/card/card-sensitive-info` | Retrieve sensitive card details. |
| [Activate Physical Card](card.md#activate-physical-card) | `/v1/card/activate-physical` | Activate a physical card. |
| [Get Change PIN Model](card.md) | `/v1/card/get-change-pin-model` | Retrieve the data required to change a card PIN. |
| [Change Card PIN](card.md) | `/v1/card/change-pin` | Change a card PIN. |
| [Replace Card](card.md#replace-card) | `/v1/card/replace` | Replace an existing card. |
| [Change Card Purchase Limit](card.md#change-card-purchase-limit) | `/v1/card/limitChange` | Update a card's purchase limit. |
| [Reject Transaction](card.md#reject-transaction) | `/v1/card/txn-verification-decline` | Decline a transaction verification request. |
| [Confirm Transaction](card.md#confirm-transaction) | `/v1/card/txn-verification-confirm` | Confirm a transaction verification request. |
| [Top Up Card](card-account.md#top-up-card) | `/v1/cardaccount/topup` | Transfer funds to a card account. |
| [Query Card Account Transactions](card-account.md#query-card-account-transactions) | `/v1/cardaccount/transactions` | Retrieve card account transactions. |
