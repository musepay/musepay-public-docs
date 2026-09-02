---
description: Set up API access and make your first MusePay integration decisions.
---

# Getting Started

The MusePay API follows REST conventions. Endpoints use resource-oriented URLs, accept JSON request bodies, return JSON responses, and use standard HTTP methods and response codes.

## Integration checklist

1. Review [Supported Assets](integration/supported-assets.md) to confirm the currencies and networks required by your product.
2. Follow [Authentication](integration/authentication.md) to generate your RSA key pair, upload the public key, and sign API requests.
3. Choose an API from the [API Reference](reference/api-reference/README.md) and review its request parameters and response objects.
4. Implement the relevant [webhooks](webhook/README.md) so your system can react to asynchronous order and card events.
5. Test the complete flow before enabling it for your customers.

{% hint style="info" %}
Keep private keys in a secure server-side environment. Never expose them in browser or mobile application code.
{% endhint %}

## Choose an integration

### Acquiring API

Accept crypto payments using either a reusable address for each user with Wallet Mode or a temporary address for each order with Checkout Mode. The guide also covers multi-chain checkout, specified-chain checkout, payment amount differences, and webhook-based reconciliation.

{% content-ref url="integration/acquiring-api/" %}
[Acquiring API Integration](integration/acquiring-api/)
{% endcontent-ref %}

### Card API

Create cardholders, issue and manage cards, fund card accounts, and handle card transaction verification. Follow the integration workflows first, then use the Card API Reference for endpoint details.

{% content-ref url="integration/card-api/" %}
[Card API Integration](integration/card-api/)
{% endcontent-ref %}

### Fiat Payout API

Send fiat currency from your USDT balance to third-party bank accounts. The integration guide explains how to discover supported routes, create a quote, submit the payout, and track its asynchronous status.

{% content-ref url="integration/fiat-payout-api/" %}
[Fiat Payout API Integration](integration/fiat-payout-api/)
{% endcontent-ref %}
