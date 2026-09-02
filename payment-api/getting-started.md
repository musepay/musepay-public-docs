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

## Building a card program?

Use the [Card API integration guide](integration/card-api/README.md) for the end-to-end workflow, then consult the Card API reference for endpoint details.
