# 卡片

#### **卡账户交易**

<table><thead><tr><th width="193.66666666666666">参数</th><th width="118">类型</th><th>说明</th></tr></thead><tbody><tr><td>type</td><td>String</td><td><p><em><strong>APPLY_AUDIT</strong></em>: 卡片申请消息 <em><strong>CARD_TOP_UP</strong></em>: 卡片充值订单消息 <em><strong>CARD_TO_WALLET</strong></em>: 卡转钱包订单消息 </p><p><em><strong>CARD_BILL_TRANSACTION</strong></em>: 卡片账单交易消息</p></td></tr><tr><td>data</td><td> Object</td><td>特定操作的消息，请参见<strong>下文</strong>。</td></tr><tr><td>sign</td><td>String</td><td>Base64 编码的签名字符串。</td></tr></tbody></table>

#### 卡片申请消息

<table><thead><tr><th width="193.66666666666666">参数</th><th width="118">类型</th><th>说明</th></tr></thead><tbody><tr><td>applyId</td><td>String</td><td>卡片申请 ID。</td></tr><tr><td>request_id</td><td>String</td><td>由合作伙伴提供的卡片申请外部 ID。</td></tr><tr><td>status</td><td>String</td><td>申请状态，请参见 <a href="../enums/apply-status.md">申请状态</a></td></tr></tbody></table>

#### 卡片订单消息

<table><thead><tr><th width="193.66666666666666">参数</th><th width="118">类型</th><th>说明</th></tr></thead><tbody><tr><td>orderNo</td><td>String</td><td>交易 ID。</td></tr><tr><td>requestId</td><td>String</td><td>由合作伙伴提供的交易外部 ID。</td></tr><tr><td>orderType</td><td>String</td><td>充值或转入钱包</td></tr><tr><td>orderCurrency</td><td>String</td><td>与卡片订单关联的币种。</td></tr><tr><td>orderAmount</td><td>String</td><td>订单处理的应收金额。</td></tr><tr><td>fee</td><td>String</td><td>服务费金额。</td></tr><tr><td>paymentAmount</td><td>String</td><td>实际支付金额。</td></tr><tr><td>feeCurrency</td><td>String</td><td>费用币种</td></tr><tr><td>status</td><td>String</td><td>交易状态，请参见 <a data-mention href="../enums/top-up-status.md">top-up-status.md</a></td></tr><tr><td>rate</td><td>String</td><td>涉及兑换时的汇率。</td></tr></tbody></table>

#### 卡片账单交易消息<br>

<table><thead><tr><th width="210.66666666666666">参数</th><th width="125">类型</th><th>说明</th></tr></thead><tbody><tr><td>detailId</td><td>String</td><td>卡账户交易 ID</td></tr><tr><td>cardId</td><td>String</td><td>用于发起该交易的卡片 ID。</td></tr><tr><td>txCreatedAt</td><td>Long</td><td>交易首次记入账户的日期/时间</td></tr><tr><td>txStatus</td><td>String</td><td><p>卡账单交易状态</p><p>请参见 <a href="../enums/card-transaction-status.md">交易状态</a></p></td></tr><tr><td>txPostedAt</td><td>Long</td><td>交易入账的日期/时间</td></tr><tr><td>txType</td><td>String</td><td>请参见 <a href="../enums/card-transaction-type.md">交易类型</a></td></tr><tr><td>txCurrency</td><td>String</td><td>以卡账户基准币种表示的交易币种</td></tr><tr><td>txAmount</td><td>Number</td><td>服务费金额。</td></tr><tr><td>txMerchant</td><td>Object</td><td>此字段提供交易发生商户的信息（仅适用于 <code>charge</code> 交易）。</td></tr><tr><td>txAuthorization</td><td>Object</td><td>授权信息，仅适用于 <code>charge</code> 交易</td></tr><tr><td>txEntryType</td><td>String</td><td>分录类型，表示该交易导致卡账户余额贷记还是借记。<br><code>DEBIT</code> 交易表示向账户增加正值（例如积分奖励、退款）；<code>CREDIT</code> 交易表示从账户余额中扣除负值（例如购买、利息费用）。</td></tr></tbody></table>

#### 卡交易验证码消息

_\*仅对部分卡片有效。_

<table><thead><tr><th width="210.66666666666666">参数</th><th width="125">类型</th><th>说明</th></tr></thead><tbody><tr><td>userId</td><td>Long</td><td>用户 ID</td></tr><tr><td>cardId</td><td>String</td><td>用于发起该交易的卡片 ID。</td></tr><tr><td>codeToken</td><td>String</td><td>该消息的唯一 Token</td></tr><tr><td>codeType</td><td>String</td><td><p>验证码类型：</p><ul><li><strong>OTP</strong> ：<strong>用于交易验证的一次性密码</strong></li><li><strong>OTP_URL：验证 URL</strong> </li><li><strong>OOB : 带外验证</strong></li></ul></td></tr><tr><td>codeContent</td><td>Object</td><td>验证码信息</td></tr><tr><td>expireTime</td><td>String</td><td>验证码过期时间</td></tr></tbody></table>
