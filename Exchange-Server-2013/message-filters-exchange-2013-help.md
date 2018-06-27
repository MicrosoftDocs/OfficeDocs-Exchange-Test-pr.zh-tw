---
title: '訊息篩選器: Exchange 2013 Help'
TOCTitle: 訊息篩選器
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 50473710
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 訊息篩選器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

篩選佇列中產生的郵件的不同檢視。藉由指定篩選準則，您可以快速找出郵件並採取動作。當電子郵件訊息傳送給多個收件者之後時，郵件可能位於多個佇列。當您依編製郵件內容篩選時，您可以找到郵件跨所有佇列。下列案例是您如何使用訊息篩選器來管理郵件流程的範例：

  - 提交佇列 Mailbox server 或從網際網路接收電子郵件的 Edge Transport server 上有大量的傳遞佇列的郵件。許多郵件都有相同的主旨。因此，您懷疑垃圾郵件會被傳送至您的組織。您可以建立篩選器來檢視符合主旨準則的所有郵件。如果您決定郵件是垃圾郵件，您可以選取將其全部並從傳遞佇列刪除而不傳送 NDR。

  - 使用者報告的郵件流程緩慢。您檢查佇列並查看有隨機主旨的許多訊息顯示給即將從單一的網域。您可以建立篩選器來檢視該網域中所有已排入佇列的郵件。如果您決定郵件是垃圾郵件，您可以選取將其全部並加以刪除佇列而不傳送 NDR。

## 郵件內容作為篩選器

您可以使用編製郵件內容來建立篩選和尋找符合指定的條件的郵件。您可以在佇列檢視器，或使用*Filter*參數的郵件管理指令程式來建立篩選器。請注意郵件管理指令程式支援多個比佇列檢視器可篩選的內容。下表列出您可篩選的郵件內容和值會與這些屬性相關聯。

### 篩選郵件時所使用的郵件內容

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>佇列檢視器郵件內容</th>
<th>命令介面訊息屬性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>接收日期</strong></p></td>
<td><p><code>DateReceived</code></p></td>
<td><p>郵件被放入佇列的日期/時間。</p></td>
</tr>
<tr class="even">
<td><p>不適用</p></td>
<td><p><code>DeferReason</code></p></td>
<td><p>此屬性會識別已延遲郵件的原因。如果未延遲郵件，這個屬性具有值<code>None</code>。延期的訊息會因收件者解析期間所發生暫時性錯誤傳回至提交佇列。如需延期郵件的詳細資訊，請參閱<a href="recipient-resolution-exchange-2013-help.md">收件者的解決方法</a>。可能的值為：</p>
<p><code>AD Transient Failure During Content Conversion</code></p>
<p><code>AD Transient Failure During Resolve</code></p>
<p><code>Agent</code></p>
<p><code>Ambiguous Recipient</code></p>
<p><code>Loop Detected</code></p>
<p><code>Marked As Retry Delivery If Rejected</code></p>
<p><code>Rerouted By Store Driver</code></p>
<p><code>Storage Transient Failure During Content Conversion</code></p>
<p><code>Transient Failure</code></p>
<p><code>Target Site Inbound Mail Disabled</code></p>
<p><code>Recipient Thread Limit Exceeded</code></p>
<p><code>Transient Attribution Failure</code></p>
<p><code>Transient Accepted Domains Load Failure</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>到期時間</strong></p></td>
<td><p><code>ExpirationTime</code></p></td>
<td><p>此內容包含郵件的到期日期/時間，屆時若無法傳遞郵件將會從佇列中刪除郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>寄件者地址</strong></p></td>
<td><p><code>FromAddress</code></p></td>
<td><p>此內容包含寄件者的 SMTP 位址。</p></td>
</tr>
<tr class="odd">
<td><p>不適用</p></td>
<td><p><code>Identity</code></p></td>
<td><p>此屬性是識別<em>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</em>的表單中的郵件。如需詳細資訊請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的 「 郵件識別碼 」 一節。</p></td>
</tr>
<tr class="even">
<td><p><strong>網際網路郵件識別碼</strong></p></td>
<td><p><code>InternetMessageId</code></p></td>
<td><p>此屬性包含位於郵件標頭<code>Message-ID:</code>標頭欄位的值。此值以表示包含 GUID 以及傳送的 SMTP 伺服器的 FQDN 的電子郵件地址。例如：</p>
<p><code>&lt;67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>上個錯誤</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>此屬性包含一個錯誤的記錄訊息的文字。例如， <code>A matching connector cannot be found to route the external recipient</code>。</p></td>
</tr>
<tr class="even">
<td><p>不適用</p></td>
<td><p><code>MessageLatency</code></p></td>
<td><p>此屬性包含經過的時間經過當郵件先輸入提交佇列在伺服器上，還是當郵件被指定佇列中。此值會使用語法<em>hh:mm:ss.ff</em>其中<em>hh</em> = 小時、 <em>mm</em> = 分鐘、 <em>ss</em> = 第二及<em>ff</em> = 一秒的分數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>郵件來源名稱</strong></p></td>
<td><p><code>MessageSourceName</code></p></td>
<td><p>此屬性包含的文字字串，表示送出至佇列的訊息傳輸元件名稱。例如，如果發生透過接收連接器的郵件，值為： <code>SMTP:</code><em>&lt;ConnectorName&gt;</em>。傳遞狀態通知 (DSN) 郵件時，此值為<code>DSN</code>。</p></td>
</tr>
<tr class="even">
<td><p>不適用</p></td>
<td><p><code>Priority</code></p></td>
<td><p>此屬性會包含在 Outlook 或Outlook Web App中之使用者所指定之郵件的優先順序。可能的值為<code>Low</code>、 <code>Normal</code>，以及<code>High</code>。如需詳細資訊，請參閱<a href="priority-queuing-exchange-2013-help.md">優先順序佇列</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>佇列識別碼</strong></p></td>
<td><p><code>Queue</code></p></td>
<td><p>此屬性會保留郵件佇列的識別。佇列識別碼使用語法<em>&lt;Server&gt;\&lt;Queue&gt;</em>。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的 「 佇列身分識別 」 一節。</p></td>
</tr>
<tr class="even">
<td><p>不適用</p></td>
<td><p><code>RetryCount</code></p></td>
<td><p>此內容可識別已嘗試將郵件傳遞至目的地的次數 (包括自動或手動)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SCL</strong></p></td>
<td><p><code>SCL</code></p></td>
<td><p>垃圾郵件信賴等級 (SCL) 屬性的值會指定郵件的 SCL。有效的 SCL 項目是從 0 到 9 的整數。空的 SCL 屬性值表示郵件尚未尚未處理的內容篩選器代理程式。</p>
<p>此屬性包含垃圾郵件信賴等級 (SCL) 值的郵件。有效的 SCL 項目是從 0 到 9 和-1 的整數。如需詳細資訊，請參閱<a href="spam-confidence-level-threshold-exchange-2013-help.md">垃圾郵件信賴等級閾值</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>大小 (KB)</strong></p></td>
<td><p><code>Size</code></p></td>
<td><p>此內容指定郵件的大小。</p></td>
</tr>
<tr class="odd">
<td><p><strong>來源 IP</strong></p></td>
<td><p><code>SourceIP</code></p></td>
<td><p>此屬性包含送出保留郵件佇列中的 Exchange 伺服器的訊息之伺服器的 IP 位址。地址可能是遠端 SMTP 伺服器的 IP 位址或本機 Exchange 伺服器的 IP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>狀態</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>此屬性會指出目前的郵件狀態。訊息可以有一個下的 [狀態] 值：</p>
<p><code>Active</code></p>
<p><code>Locked</code></p>
<p><code>None</code></p>
<p><code>Pending Remove</code></p>
<p><code>Pending Suspend</code></p>
<p><code>Ready</code></p>
<p><code>Retry</code></p>
<p><code>Suspended</code></p>
<p>如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題中的「郵件內容」一節。</p></td>
</tr>
<tr class="odd">
<td><p><strong>主旨</strong></p></td>
<td><p><code>Subject</code></p></td>
<td><p>此內容指出在郵件標頭的 <code>Subject:</code> 標頭欄位中找到的郵件主旨。</p></td>
</tr>
</tbody>
</table>

