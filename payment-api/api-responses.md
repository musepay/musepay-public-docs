# API Responses

### HTTP Status Code <a href="#http-status-code" id="http-status-code"></a>

* **200** - `OK` - Request processed as expected.
* **400** - `INVALID_REQUEST` - Request is not well-formed, violates schema or incorrect fields.
* **401** - `NOT_AUTHORIZED` - The API key doesn't match the signature or doesn't have permissions to perform the request.
* **403** - `FORBIDDEN` - The API key's permissions doesn't match the needed permission to complete the request.
* **404** - `RESOURCE_NOT_FOUND` - The requested resource doesn't exist.
* **429** - `RATE_LIMIT_REACHED` - Too many requests. Blocked due to rate limiting.
* **5XX** - Something went wrong on ToPay's end



### API Error Codes

<table><thead><tr><th width="130.66666666666666">Error Code</th><th>Constant</th><th>Desc</th></tr></thead><tbody><tr><td>406</td><td>SIGN_ERROR</td><td></td></tr><tr><td>412</td><td>WRONG_TIMESTAMP_OR_NONCE</td><td></td></tr><tr><td>5004</td><td>USER_STATUS_INVALID</td><td></td></tr><tr><td>7000</td><td>ORDER_NOT_EXIST</td><td></td></tr><tr><td>7002</td><td>CURRENCY_NOT_SUPPORT</td><td></td></tr><tr><td>202206</td><td>QUOTA_MIN_CHECK_FAIL</td><td></td></tr><tr><td>202211</td><td>UNSUPPORTED_CURRENCY</td><td></td></tr><tr><td>202224</td><td>DOUBLE_PAYMENT</td><td></td></tr><tr><td>202203</td><td>INSUFFICIENT_BALANCE</td><td></td></tr><tr><td>202212</td><td>ORDER_AMOUNT_MUST_MORE_THAN_SERVICE_FEE</td><td></td></tr><tr><td>2204002</td><td>NO_SPECIFIED_FEE_RULE</td><td></td></tr><tr><td>206003</td><td>PAYOUT_METHOD_INVALID</td><td>Please check your request parameters: country, payout_method, bankcode, walletcode</td></tr><tr><td></td><td></td><td></td></tr></tbody></table>
