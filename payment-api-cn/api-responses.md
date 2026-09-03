# API 响应

### HTTP 状态码 <a href="#http-status-code" id="http-status-code"></a>

* **200** - `OK` - 请求已按预期处理。
* **400** - `INVALID_REQUEST` - 请求格式不正确、不符合数据结构要求或包含错误字段。
* **401** - `NOT_AUTHORIZED` - API Key 与签名不匹配，或没有执行该请求的权限。
* **403** - `FORBIDDEN` - API Key 不具备完成该请求所需的权限。
* **404** - `RESOURCE_NOT_FOUND` - 请求的资源不存在。
* **429** - `RATE_LIMIT_REACHED` - 请求过多，已触发频率限制。
* **5XX** - MusePay 服务端发生错误



### API 错误码

<table><thead><tr><th width="130.66666666666666">错误码</th><th>常量</th><th>说明</th></tr></thead><tbody><tr><td>406</td><td>SIGN_ERROR</td><td></td></tr><tr><td>412</td><td>WRONG_TIMESTAMP_OR_NONCE</td><td></td></tr><tr><td>5004</td><td>USER_STATUS_INVALID</td><td></td></tr><tr><td>7000</td><td>ORDER_NOT_EXIST</td><td></td></tr><tr><td>7002</td><td>CURRENCY_NOT_SUPPORT</td><td></td></tr><tr><td>202206</td><td>QUOTA_MIN_CHECK_FAIL</td><td></td></tr><tr><td>202211</td><td>UNSUPPORTED_CURRENCY</td><td></td></tr><tr><td>202224</td><td>DOUBLE_PAYMENT</td><td></td></tr><tr><td>202203</td><td>INSUFFICIENT_BALANCE</td><td></td></tr><tr><td>202212</td><td>ORDER_AMOUNT_MUST_MORE_THAN_SERVICE_FEE</td><td></td></tr><tr><td>2204002</td><td>NO_SPECIFIED_FEE_RULE</td><td></td></tr><tr><td>206003</td><td>PAYOUT_METHOD_INVALID</td><td>请检查请求参数：country、payout_method、bankcode、walletcode</td></tr><tr><td></td><td></td><td></td></tr></tbody></table>
