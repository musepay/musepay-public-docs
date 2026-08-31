# How to Issue a Card

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

### 1. Get Card Product ID

When issuing a card, the productId must be specified and determines the card product to issue. The card product determines the card type, card face, card features, benefits, interest rates, capabilties, etc. The list of available productIds is static will be provided by your solution manager. Also you can retrieve the productIds from the agent's portal ([https://agent.musepay.io/](https://agent.musepay.io/)).

### 2. Create Card Holder

Go to Page  [Getting Started](getting-started.md) and set up your API access key. and then perform API requests to create user as card holder in accordance to the specification provided in [User](reference/api-reference/card-api/card-user.md) endpoints.

### 3. Apply a Card

Once a card holder is created, you can continue to create card application in accordance to the specification provided in [Card](reference/api-reference/card-api/card.md#apply-card) endpoints.

### 4. Top Up

* Firstly, you need to recharge a certain amount of crypto assets to your agent account. Go to the agent's portal and navigate to Balance -> Deposit Coin as follow, where you can obtain a crypto address. After the cryptocurrency is confirmed on chain, your agent account will have a balance.

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

*   Then, you can Top up in accordance to the specification provided in [Top Up](reference/api-reference/card-api/card-account.md#top-up-card) endpoints. the system will transfer the specified amount from your agent account to your designated card according to your api request.

    <br>

