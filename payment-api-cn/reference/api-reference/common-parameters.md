# 通用参数

**每个请求的 Body 中都必须包含以下参数：**

<table><thead><tr><th width="154">参数</th><th width="104">类型</th><th>说明</th></tr></thead><tbody><tr><td><em>partner_id</em></td><td>String</td><td>MusePay 为您分配的账户 ID。</td></tr><tr><td><em>sign_type</em></td><td>String</td><td>固定值：`RSA`。</td></tr><tr><td><em>timestamp</em></td><td>String</td><td>请求发起时间，为从 Unix Epoch 开始计算的秒数。</td></tr><tr><td><em>nonce</em></td><td>String</td><td>唯一随机数或字符串。每个 API 请求都必须使用不同的 nonce。</td></tr><tr><td><em>sign</em></td><td>String</td><td>Base64 编码的签名字符串。</td></tr></tbody></table>
