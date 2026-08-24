# Common Parameters

**Every request must contain the following parameters in the body:**

<table><thead><tr><th width="154">Parameters</th><th width="104">Type</th><th>Desc</th></tr></thead><tbody><tr><td><em>partner_id</em></td><td>String</td><td>The ID of your Account allocated from MusePay.</td></tr><tr><td><em>sign_type</em></td><td>String</td><td>fixed value: "RSA".</td></tr><tr><td><em>timestamp</em></td><td>String</td><td>The time at which the request was called, in seconds since Epoch.</td></tr><tr><td><em>nonce</em></td><td>String</td><td>Unique random number or string. Each API request needs to have a different nonce.</td></tr><tr><td><em>sign</em></td><td>String</td><td>Base64 encoded signature string.</td></tr></tbody></table>
