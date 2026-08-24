# Card Transactions Verification

This document describes the workflow for verifying card transactions via webhook integration. It outlines how partners can receive transaction verification messages and interact with clients to complete the verification process.

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### Workflow Overview

#### Step 1: Verification Trigger

* When a transaction requires verification (such as 3DS or OTP), VISA triggers the process.
* MuseCard receives the verification event from VISA.

#### Step 2: Webhook Notification to Partner System

MuseCard sends a webhook notification to the Partner System:

* CARD\_TX\_OOB: Out-of-band verification (client confirmation required).
* CARD\_TX\_OTP: One-time password (OTP) verification.
* CARD\_TX\_3DS\_URL: 3D Secure verification URL.

#### Step 3: Client Interaction

The Partner System forwards the verification message to the client:

* For CARD\_TX\_OTP, the client inputs the OTP code.
* For CARD\_TX\_3DS\_URL, the client clicks the verification URL to complete the 3D Secure process.
* For CARD\_TX\_OOB, the Partner System pushes a message to the client for manual confirmation.



### 2. CARD\_TX\_OOB Model (Out-of-Band Verification)

1. The client receives the verification request via the Partner System.
2. The client confirms or declines the transaction.
3. The Partner System sends the result to MuseCard via API:
   * POST [/txn-verification-confirm](reference/api-reference/card.md#confirm-transaction) — to confirm the transaction.
   * POST [/txn-verification-decline](reference/api-reference/card.md#reject-transaction) — to decline the transaction.
4. MuseCard processes the response and sends the result to VISA via callback.

***

### 3. Key Notes

* All webhook events are sent to the Partner System in real time.
* The Partner System is responsible for delivering the message to the client.
* Timely processing of verification responses is crucial to avoid transaction delays.

