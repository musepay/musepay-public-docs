---
description: Restrict API access to approved server IP addresses.
---

# IP Whitelisting

MusePay can restrict requests made with an API key so that they are accepted only from approved IP addresses.

To configure an IP whitelist, contact MusePay Technical Support and provide:

* The API key identifier to configure.
* The public outbound IP address of each server that will call the MusePay API.

{% hint style="warning" %}
Never send your private key to MusePay or any third party. MusePay only needs the API key identifier and the IP addresses to configure the whitelist.
{% endhint %}

Use stable outbound IP addresses. Requests originating from an address that is not on the whitelist will not be accepted.
