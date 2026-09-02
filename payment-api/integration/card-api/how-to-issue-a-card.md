# How to Issue a Card

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

### 1. Get Card Product ID

When issuing a card, the productId must be specified and determines the card product to issue. The card product determines the card type, card face, card features, benefits, interest rates, capabilties, etc. The list of available productIds is static will be provided by your solution manager. Also you can retrieve the productIds from the Partner Portal ([https://agent.musepay.io/](https://agent.musepay.io/)).

### 2. Create Card Holder

Follow [Authentication](../authentication.md) to set up API access. Then create a cardholder using the [Card User](../../reference/api-reference/card-api/card-user.md) endpoints.

### 3. Apply a Card

Once the cardholder is created, submit a card application using the [Apply Card](../../reference/api-reference/card-api/card.md#apply-card) endpoint.

### 4. Top Up

* Firstly, you need to recharge a certain amount of crypto assets to your partner basic account. Go to the Partner Portal and navigate to Balance -> Deposit Coin as follow, where you can obtain a crypto address. After the cryptocurrency is confirmed on chain, your partner basic account will have a balance.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

*   Then use the [Top Up Card](../../reference/api-reference/card-api/card-account.md#top-up-card) endpoint. MusePay transfers the specified amount from your partner basic account to the selected card account.

    <br>
