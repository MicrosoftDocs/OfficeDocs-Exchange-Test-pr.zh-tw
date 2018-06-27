---
title: '傳輸規則動作: Exchange 2013 Help'
TOCTitle: 郵件流程規則動作
ms:assetid: 5d11a955-b1cc-4150-a0b9-a8cc48ba9bde
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998315(v=EXCHG.150)
ms:contentKeyID: 50473303
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳輸規則動作

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-05-03_

郵件流程規則 （也稱為傳輸規則） 的動作指定想要執行符合的規則條件的郵件。例如，您可以建立將特定的寄件者的郵件轉寄給仲裁，或將免責聲明或個人化的簽章新增至所有外寄郵件的規則。

動作通常需要額外的屬性。例如，當此規則會將郵件重新導向，您需要指定將郵件重新導向的位置。有些動作有多個可用或必要的屬性。例如，當此規則會將標頭欄位新增至郵件標頭，您需要指定的名稱和標頭的值。當規則新增至郵件免責聲明時，您必須指定免責聲明文字，但您也可以指定要插入的文字，或如果免責聲明無法新增至郵件。一般而言，您可以設定多個動作的規則，但某些動作不存在。例如，一項規則無法拒絕並將相同的郵件重新導向。

如需Exchange Server 2013中的郵件流程規則的詳細資訊，請參閱[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。

如需條件和例外狀況的郵件流程規則的詳細資訊，請參閱[傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)。

如需在Exchange Online或Exchange Online Protection的郵件流程規則動作的詳細資訊，請參閱[郵件流程規則動作在 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj919237\(v=exchg.150\))或[郵件流程規則動作在 Exchange Online Protection](https://technet.microsoft.com/zh-tw/library/jj920117\(v=exchg.150\))。

## 在信箱伺服器上的郵件流程規則動作

下表說明在信箱伺服器上的郵件流程規則中可用的動作。有效的每個屬性的值所述的屬性值\] 區段中。

**附註：**

  - Exchange 系統管理中心 (EAC) 中選取動作之後，最終顯示在 \[**執行下列動作**\] 欄位的值是常與您所選取的 click 路徑不同。此外，當您建立新規則，您可以有時 （根據您所選取項目） 自範本 （已篩選清單的動作），而不是遵循完成 click 路徑選取簡短的動作名稱。簡短的名稱與完整按一下值顯示在表格中的 EAC 中\] 欄中的路徑。

  - **Get-TransportRuleAction**指令程式所傳回的動作的名稱會不同於相對應的參數名稱和多個參數可能需要的動作。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>在 EAC 中的動作</th>
<th>在Exchange 管理命令介面 action 參數</th>
<th>屬性</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>核准的郵件轉寄給這些人員</strong></p>
<p><strong>轉寄郵件核准</strong>&gt;<strong>給這些人員</strong></p></td>
<td><p><em>ModerateMessageByUser</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>轉寄至指定之仲裁者的郵件以附件形式包裝在核准要求中。如需詳細資訊，請參閱<a href="common-message-approval-scenarios-exchange-2013-help.md">常見的郵件核准案例</a>。您不能作為仲裁通訊群組。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>核准的郵件轉寄給寄件者的經理</strong></p>
<p><strong>轉寄郵件核准</strong>&gt;<strong>給寄件者的經理</strong></p></td>
<td><p><em>ModerateMessageByManager</em></p></td>
<td><p>不適用</p></td>
<td><p>將郵件轉寄給寄件者經理進行核准。</p>
<p>此巨集指令只適用於Active Directory定義寄件者<strong>Manager</strong>屬性則。否則請郵件傳遞給而不進行仲裁收件者。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>將郵件重新導向至這些收件者</strong></p>
<p><strong>若要將郵件重新導向</strong>&gt;<strong>這些收件者</strong></p></td>
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>將郵件重新導向至指定的收件者。郵件無法傳遞至原始收件者並不通知傳送給寄件者或原始收件者。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>以說明來拒絕接收郵件</strong></p>
<p><strong>封鎖郵件</strong>&gt;<strong>拒絕此郵件並包含說明</strong></p></td>
<td><p><em>RejectMessageReasonText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>會傳回給寄件者具有指定之文字的未傳遞回報 （也稱為 NDR 或彈跳訊息） 中的拒絕原因的訊息。收件者不會收到原始訊息或通知。</p>
<p>使用預設增強型狀態程式碼是<code>5.7.1</code>。</p>
<p>當您建立或修改Exchange 管理命令介面中的規則時，您可以使用<em>RejectMessageEnhancedStatusCode</em>參數指定的 DSN 代碼。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>以增強型狀態碼拒絕接收郵件</strong></p>
<p><strong>封鎖郵件</strong>&gt;<strong>拒絕此郵件以增強型的狀態碼</strong></p></td>
<td><p><em>RejectMessageEnhancedStatusCode</em></p></td>
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>會傳回至具有指定增強型的傳遞狀態通知 (DSN) 程式碼 NDR 的寄件者的訊息。收件者不會收到原始訊息或通知。</p>
<p>有效的 DSN 代碼為<code>5.7.1</code>或透過<code>5.7.999</code><code>5.7.900</code> 。</p>
<p>使用預設原因文字是<code>Delivery not authorized, message refused</code>。</p>
<p>當您建立或修改Exchange 管理命令介面中的規則時，您可以藉由使用<em>RejectMessageReasonText</em>參數指定拒絕原因文字。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>刪除郵件而不通知任何人</strong></p>
<p><strong>封鎖郵件</strong>&gt;<strong>刪除郵件而不通知任何人</strong></p></td>
<td><p><em>DeleteMessage</em></p></td>
<td><p>不適用</p></td>
<td><p>以無訊息方式將郵件而不傳送通知給收件者或寄件者。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>新增至 [密件副本] 方塊中的收件者</strong></p>
<p><strong>新增的收件者</strong>&gt; <strong>[密件副本] 方塊</strong></p></td>
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>將一或多個收件者新增至郵件的 [ <strong>Bcc</strong> ] 欄位。原始收件者不會收到通知，並不能看到其他地址。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>新增收件者到 [收件者] 方塊</strong></p>
<p><strong>新增的收件者</strong>&gt;<strong>至 [收件者] 方塊中</strong></p></td>
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>將一個或多個收件者新增至郵件的 [ <strong>To</strong> ] 欄位。原始收件者可以看到其他地址。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>將收件者新增至 [副本] 方塊</strong></p>
<p><strong>新增的收件者</strong>&gt; <strong>[副本] 方塊</strong></p></td>
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>將一個或多個收件者新增至郵件的 [ <strong>Cc</strong> ] 欄位。原始收件者可以看到其他地址。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>將寄件者的管理員新增為收件者</strong></p>
<p><strong>新增的收件者</strong>&gt;<strong>新增為收件者的寄件者的管理員</strong></p></td>
<td><p><em>AddManagerAsRecipientType</em></p></td>
<td><p><code>AddedManagerAction</code></p></td>
<td><p>將郵件的寄件者的管理員新增為指定的收件者類型 （<strong>To</strong>、 <strong>Cc</strong>、 <strong>Bcc</strong>） 或將郵件重新導向至寄件者的經理而不通知寄件者或收件者。</p>
<p>如果寄件者<strong>Manager</strong>屬性定義中Active Directory，只適用於此巨集指令。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>附加免責聲明</strong></p>
<p><strong>套用至郵件免責聲明</strong>&gt;<strong>附加免責聲明</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>第一個屬性：<code>DisclaimerText</code></p>
<p>第二個屬性： <code>DisclaimerFallbackAction</code></p>
<p>第三個屬性 (僅限Exchange 管理命令介面 )： <code>DisclaimerTextLocation</code></p></td>
<td><p>將之指定的 HTML 免責聲明套用之郵件的結尾。</p>
<p>當您建立或修改Exchange 管理命令介面中的規則時，請搭配值<code>Append</code><em>ApplyHtmlDisclaimerTextLocation</em>參數。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>加上免責聲明</strong></p>
<p><strong>套用至郵件免責聲明</strong>&gt;<strong>前面加上免責聲明</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>第一個屬性：<code>DisclaimerText</code></p>
<p>第二個屬性： <code>DisclaimerFallbackAction</code></p>
<p>第三個屬性 (僅限Exchange 管理命令介面 )： <code>DisclaimerTextLocation</code></p></td>
<td><p>將指定的 HTML 免責聲明套用至訊息的開頭。</p>
<p>當您建立或修改Exchange 管理命令介面中的規則時，請搭配值<code>Prepend</code><em>ApplyHtmlDisclaimerTextLocation</em>參數。</p>
<p></p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>刪除此標頭</strong></p>
<p><strong>修改訊息屬性</strong>&gt;<strong>移除郵件標頭</strong></p></td>
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>郵件標頭中移除指定的標頭] 欄位。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>將郵件標頭設為此值</strong></p>
<p><strong>修改訊息屬性</strong>&gt;<strong>設定郵件標頭</strong></p></td>
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>第一個屬性： <code>MessageHeaderField</code></p>
<p>第二個屬性： <code>String</code></p></td>
<td><p>新增或修改的郵件標頭中的指定的標頭欄位並設定的標頭欄位至指定的值。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>套用郵件分類</strong></p>
<p><strong>修改訊息屬性</strong>&gt;<strong>套用郵件分類</strong></p></td>
<td><p><em>ApplyClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>對郵件套用指定的郵件分類。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>若要設定的垃圾郵件信賴等級 (SCL)</strong></p>
<p><strong>修改訊息屬性</strong>&gt;<strong>設定垃圾郵件信賴等級 (SCL)</strong></p></td>
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>將郵件的垃圾郵件信賴等級 (SCL) 設定為指定的值。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>套用權限保護到具有下列條件的郵件</strong></p>
<p><strong>修改郵件安全性</strong>&gt;<strong>套用權限保護</strong></p></td>
<td><p><em>ApplyRightsProtectionTemplate</em></p></td>
<td><p><code>RMSTemplate</code></p></td>
<td><p>對郵件套用指定的 Rights Management Services (RMS) 範本。</p>
<p>RMS 需要Exchange企業用戶端存取授權 (Cal) 的每個信箱。如需 Cal 的詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 授權</a>。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>需要 TLS 加密</strong></p>
<p><strong>修改郵件安全性</strong>&gt;<strong>需要 TLS 加密</strong></p></td>
<td><p><em>RouteMessageOutboundRequireTls</em></p></td>
<td><p><code>n/a</code></p></td>
<td><p>強制輸出郵件路由傳送透過 TLS 加密連線。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>在郵件主旨前面加上</strong></p></td>
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>將指定的文字新增至郵件的<strong>Subject</strong>欄位的開頭。請考慮使用空格或冒號 （:） 為指定之文字的最後一個字元來區分從原始的主旨文字。</p>
<p>若要防止相同的字串新增至已包含主體 （例如回覆） 中的文字的郵件，新增<strong>主旨包含</strong>(<em>ExceptIfSubjectContainsWords</em>) 例外狀況的規則。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>以原則提示通知寄件者</strong></p></td>
<td><p><em>NotifySender</em></p>
<p><em>RejectMessageReasonText</em></p>
<p><em>RejectMessageEnhancedStatusCode</em>(僅限Exchange 管理命令介面 )</p></td>
<td><p>第一個屬性： <code>NotifySenderType</code></p>
<p>第二個屬性： <code>String</code></p>
<p>第三個屬性 (僅限Exchange 管理命令介面 )： <code>DSNEnhancedStatusCode</code></p></td>
<td><p>通知寄件者或在郵件符合 DLP 原則時封鎖訊息。</p>
<p>當您使用此巨集指令時，您需要使用<strong>郵件包含敏感資訊</strong>（<em>MessageContainsDataClassification</em>條件。</p>
<p>當您建立或修改Exchange 管理命令介面中的規則時， <em>RejectMessageReasonText</em>參數是選擇性的。如果您未使用此參數，則會使用預設文字<code>Delivery not authorized, message refused</code> 。</p>
<p>在Exchange 管理命令介面中，您也可以使用<em>RejectMessageEnhancedStatusCode</em>參數指定增強型的狀態程式碼。如果您未使用此參數，則會使用預設增強型狀態的程式碼<code>5.7.1</code> 。</p>
<p>此動作會限制其他條件、 例外狀況和您可以設定規則的動作。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>產生附隨報告並傳送至</strong></p></td>
<td><p><em>GenerateIncidentReport</em></p>
<p><em>IncidentReportContent</em></p></td>
<td><p>第一個屬性：<code>Addresses</code></p>
<p>第二個屬性：<code>IncidentReportContent</code></p></td>
<td><p>傳送含有指定收件者的指定的內容附隨報告。</p>
<p>產生附隨報告出符合您組織中的資料外洩防護 (DLP) 原則。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>以郵件通知收件者</strong></p></td>
<td><p><em>GenerateNotification</em></p></td>
<td><p><code>NotificationMessageText</code></p></td>
<td><p>會指定文字、 HTML 標籤及訊息關鍵字包含在通知訊息傳送給郵件的收件者。例如，您可以通知收件者郵件已拒絕規則，或標示為垃圾郵件和傳遞至其垃圾郵件] 資料夾。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>此規則的屬性</strong>] 區段中 &gt;<strong>此規則使用嚴重性層級的稽核</strong></p></td>
<td><p><em>SetAuditSeverity</em></p></td>
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>指定是否要：</p>
<ul>
<li><p>防止產生附隨報告和郵件追蹤記錄檔中的對應項目。</p></li>
<li><p>產生附隨報告與對應的項目在郵件追蹤記錄檔以指定的嚴重性層級 （低、 中型或高）。</p></li>
</ul></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>此規則的屬性</strong>] 區段中 &gt;<strong>停止處理其他規則</strong></p>
<p><strong>更多選項]</strong> &gt;<strong>此規則的屬性</strong>] 區段中 &gt;<strong>停止處理其他規則</strong></p></td>
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>不適用</p></td>
<td><p>會指定郵件會影響規則之後，郵件免除處理其他規則。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## Edge Transport server 上的郵件流程規則動作

小型 Mailbox server 可用的動作子集也 Edge Transport server 上但也有某些僅可用於邊際傳輸伺服器上的動作。您只可以管理中Exchange 管理命令介面本機 Edge Transport server 上的郵件流程規則讓 Edge Transport server 上有無 EAC。下表說明動作。說明內容類型的屬性值\] 區段中。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>在Exchange 管理命令介面 action 參數</th>
<th>屬性</th>
<th>描述</th>
<th>可在</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>將一或多個收件者新增至郵件的 [ <strong>To</strong> ] 欄位。原始收件者可以看到其他地址。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>將一或多個收件者新增至郵件的 [ <strong>Bcc</strong> ] 欄位。原始收件者不會收到通知，並不能看到其他地址。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>將一或多個收件者新增至郵件的 [ <strong>Cc</strong> ] 欄位。原始收件者可以看到其他地址。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>DeleteMessage</em></p></td>
<td><p>不適用</p></td>
<td><p>以無訊息方式將郵件而不傳送通知給收件者或寄件者。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>Disconnect</em></p></td>
<td><p>不適用</p></td>
<td><p>結束之間傳送的伺服器與 Edge Transport server 的 SMTP 連線且不產生 NDR。</p></td>
<td><p>只有在 edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>LogEventText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>會以指定的文字事件產生本機 Edge Transport server 的應用程式記錄檔中。項目都包含下列資訊：</p>
<ul>
<li><p><strong>層級</strong>   <code>Information</code></p></li>
<li><p><strong>來源</strong>   <code>MSExchange Messaging Policies</code></p></li>
<li><p><strong>事件識別碼</strong>   <code>4000</code></p></li>
<li><p><strong>工作類別</strong>   <code>Rules</code></p></li>
<li><p><strong>EventData</strong>   <code>The following message is logged by an action in the rules: &lt;text you specify&gt;.</code></p></li>
</ul></td>
<td><p>只有在 edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>將指定的文字新增至郵件的<strong>Subject</strong>欄位的開頭。請考慮使用空格或冒號 （:） 為指定之文字的最後一個字元來區分從原始的主旨。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>Quarantine</em></p></td>
<td><p>不適用</p></td>
<td><p>將郵件傳遞至隔離信箱中內容篩選設定 Edge Transport server 上的定義。如需詳細資訊，請參閱<a href="configure-a-spam-quarantine-mailbox-exchange-2013-help.md">設定垃圾郵件隔離信箱</a>。</p>
<p>如果未設定隔離信箱，郵件會傳回至 NDR 的寄件者。</p></td>
<td><p>只有在 edge Transport server</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>將郵件重新導向至指定的收件者。郵件無法傳遞至原始收件者並不通知傳送給寄件者或原始收件者。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>郵件標頭中移除指定的標頭] 欄位。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>第一個屬性： <code>MessageHeaderField</code></p>
<p>第二個屬性： <code>String</code></p></td>
<td><p>新增或修改的郵件標頭中的指定的標頭欄位並設定的標頭欄位至指定的值。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>將郵件的 SCL 設定為指定的值。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>SmtpRejectMessageRejectText</em></p>
<p><em>SmtpRejectMessageRejectStatusCode</em></p></td>
<td><p>第一個屬性： <code>String</code></p>
<p>第二個屬性： <code>SMTPStatusCode</code></p></td>
<td><p>結束之間傳送的伺服器與 Edge Transport server 與指定的 SMTP 狀態碼拒絕指定的文字的 SMTP 連線。收件者不會收到原始訊息或通知。</p>
<p>SMTP 狀態碼有效值為<code>400</code>透過<code>500</code> RFC 3463 中所定義的整數。</p>
<p>如果您指定拒絕文字但未指定 SMTP 狀態碼，則會使用預設的程式碼<code>550</code> 。</p>
<p>如果您指定的 SMTP 狀態碼但未指定拒絕文字時，所使用的文字是<code>Delivery not authorized, message refused</code>。</p></td>
<td><p>只有在 edge Transport server</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>不適用</p></td>
<td><p>會指定郵件會影響規則之後，郵件免除處理其他規則。</p></td>
<td><p>Mailbox server 及 Edge Transport server</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
</tbody>
</table>


## 屬性值

下表說明用於的郵件流程規則動作的屬性值。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>有效值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>AddedManagerAction</code></p></td>
<td><p>下列其中一個值：</p>
<ul>
<li><p><strong>到</strong></p></li>
<li><p><strong>[副本]</strong></p></li>
<li><p><strong>[密件副本</strong></p></li>
<li><p><strong>重新導向</strong></p></li>
</ul></td>
<td><p>會指定如何在訊息中加入寄件者的管理員。</p>
<ul>
<li><p>如果您選取 [<strong>以</strong>、 <strong>[副本</strong>] 或<strong>[密件副本</strong>、 寄件者的管理員新增為指定的欄位中的收件者。</p></li>
<li><p>如果您選取 [<strong>重新導向</strong>，郵件只傳遞給寄件者的經理而不通知寄件者或收件者。</p></li>
</ul>
<p>此巨集指令只適用於Active Directory定義寄件者<strong>Manager</strong>屬性則。</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Exchange收件者</p></td>
<td><p>動作，而您可以在組織中指定擁有郵件功能的任何物件或您可能會限制在特定的物件類型。一般而言，您可以選取多個收件者，但您只能傳送給收件者附隨報告。</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>下列其中一個值：</p>
<ul>
<li><p>取消核取 [<strong>此規則使用嚴重性層級的稽核</strong>，或<strong>未指定</strong>(<code>DoNotAudit</code>) 的值選取<strong>此規則使用嚴重性層級的稽核</strong></p></li>
<li><p><strong>低</strong></p></li>
<li><p><strong>中等</strong></p></li>
<li><p><strong>高</strong></p></li>
</ul></td>
<td><p><strong>Low</strong>、 <strong>Medium</strong>或<strong>High</strong>的值指定為指派給附隨報告和郵件追蹤記錄檔中的對應項目的重要性層級。</p>
<p>其他值防止在產生附隨報告並防止對應項目正在寫入至追蹤記錄檔的郵件。</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerFallbackAction</code></p></td>
<td><p>下列其中一個值：</p>
<ul>
<li><p><strong>文字會圍繞</strong></p></li>
<li><p><strong>略過</strong></p></li>
<li><p><strong>拒絕</strong></p></li>
</ul></td>
<td><p>會指定如果沒有免責聲明無法套用至郵件項目。偶爾位置不能變更郵件的內容 （例如將郵件加密）。會在可用的後援動作：</p>
<ul>
<li><p><strong>文字會圍繞</strong>  原始郵件會被包裝中新的郵件信封，並將免責聲明文字插入至新的訊息。此為預設值。</p>
<p><strong>附註：</strong></p>
<ul>
<li><p>後續的郵件流程規則會套用至新的郵件信封中未提供給原始郵件。因此，設定這些規則比其他規則較低優先順序。</p></li>
<li><p>如果原始郵件無法在新的郵件信封中自動換行，原始郵件無法傳遞。郵件會傳回給寄件者的 NDR。</p></li>
</ul></li>
<li><p><strong>略過</strong>  忽略此規則與郵件傳遞沒有免責聲明</p></li>
<li><p><strong>拒絕</strong>  郵件會傳回給寄件者的 NDR。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DisclaimerText</code></p></td>
<td><p>HTML 字串</p></td>
<td><p>會指定免責聲明文字，可以使用 IMG 標籤包含 HTML 標記、 內嵌階層式樣式表 (CSS) 標記及圖像。長度上限是 5000 個字元，包括標記。</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerTextLocation</code></p></td>
<td><p>單一值： <code>Append</code>或<code>Prepend</code></p></td>
<td><p>在Exchange 管理命令介面中，您可以使用<em>ApplyHtmlDisclaimerTextLocation</em>郵件中指定的免責聲明文字的位置：</p>
<ul>
<li><p><code>Append</code>  將免責聲明新增至郵件內文結尾。此為預設值。</p></li>
<li><p><code>Prepend</code>  將免責聲明新增至郵件內文結尾。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>單一 DSN 代碼值：</p>
<ul>
<li><p><code>5.7.1</code></p></li>
<li><p>透過<code>5.7.999</code><code>5.7.900</code></p></li>
</ul></td>
<td><p>指定所使用的 DSN 代碼。您可以使用<strong>New-SystemMessage</strong>指令程式來建立自訂 Dsn。</p>
<p>如果您沒有指定 DSN 碼以及拒絕理由文字，會使用預設原因文字是<code>Delivery not authorized, message refused</code>。</p>
<p>當您建立或修改Exchange 管理命令介面中的規則時，您可以藉由使用<em>RejectMessageReasonText</em>參數指定拒絕原因文字。</p></td>
</tr>
<tr class="even">
<td><p><code>IncidentReportContent</code></p></td>
<td><p>下列的一或多個值：</p>
<ul>
<li><p><strong>寄件者</strong></p></li>
<li><p><strong>收件者</strong></p></li>
<li><p><strong>主旨</strong></p></li>
<li><p><strong>[副本] 位置的分散式收件者</strong>(<code>Cc</code>)</p></li>
<li><p><strong>[密件副本位置的分散式收件者</strong>(<code>Bcc</code>)</p></li>
<li><p><strong>嚴重性</strong></p></li>
<li><p><strong>寄件者覆寫資訊</strong>(<code>Override</code>)</p></li>
<li><p><strong>比對規則</strong>(<code>RuleDetections</code>)</p></li>
<li><p><strong>False 正數報告</strong>(<code>FalsePositive</code>)</p></li>
<li><p><strong>偵測到的資料分類</strong>(<code>DataClassifications</code>)</p></li>
<li><p><strong>符合內容</strong>(<code>IdMatch</code>)</p></li>
<li><p><strong>原始的郵件</strong>(<code>AttachOriginalMail</code>)</p></li>
</ul></td>
<td><p>指定要包含在隨附報告的原始郵件屬性。您可以選擇包含這些屬性的任何組合。除了您指定的屬性、 郵件 ID 一律是包含。可用的屬性包括：</p>
<ul>
<li><p><strong>寄件者</strong>  原始郵件的寄件者。</p></li>
<li><p><strong>收件者</strong>、 <strong>[副本] 位置的分散式收件者</strong>，和<strong>[密件副本] 位置的分散式收件者</strong>之郵件的所有收件者或僅<strong>Cc</strong>或<strong>Bcc</strong>欄位中的收件者。每個屬性，附隨報告中會包含只前 10 的收件者。</p></li>
<li><p><strong>主旨</strong>  原始郵件的 [ <strong>Subject</strong> ] 欄位。</p></li>
<li><p><strong>嚴重性</strong>  觸發規則的稽核嚴重性。郵件追蹤記錄檔包含所有的稽核嚴重性層級，並可由稽核嚴重性篩選。在 EAC 中，如果清除<strong>稽核嚴重性層級與此規則</strong>] 核取方塊 （在Exchange 管理命令介面、 <em>SetAuditSeverity</em>參數值<code>DoNotAudit</code>)、 規則比對不會出現在規則報告。如果訊息已由多個規則所處理的、 最高嚴重性隨附於任何附隨報告。</p></li>
<li><p><strong>寄件者覆寫資訊</strong>  如果寄件者選擇覆寫原則提示覆寫。若寄件者提供的理由，同時包含 justification 的第一次 100 個字元。</p></li>
<li><p><strong>比對規則</strong>  郵件觸發的規則清單。</p></li>
<li><p><strong>False 正數報告</strong>  誤判如果寄件者標示郵件為誤判為原則提示。</p></li>
<li><p><strong>偵測到的資料分類</strong>  在郵件中偵測到的敏感資訊類型清單。</p></li>
<li><p><strong>符合內容</strong>  敏感資訊類型偵測到、 郵件和 150 個字元完全相符的內容相符機密資訊前後。</p></li>
<li><p><strong>原始的郵件</strong>  觸發此規則整封郵件會附加到附隨報告。</p></li>
</ul>
<p>在Exchange 管理命令介面中，您可以指定多個以逗號分隔的值。</p></td>
</tr>
<tr class="odd">
<td><p><code>MessageClassification</code></p></td>
<td><p>單一郵件分類物件</p></td>
<td><p>在 EAC 中，從清單中選取的可用的郵件分類。</p>
<p>在Exchange 管理命令介面中，使用<strong>Get-MessageClassification</strong>指令程式來查看可用的郵件分類物件。</p></td>
</tr>
<tr class="even">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>單一字串</p></td>
<td><p>指定要新增、 移除或修改的 SMTP 郵件標頭欄位。</p>
<p><em>郵件標頭</em>是在郵件中的必要及選用的標頭欄位的集合。標頭欄位的範例是<strong>To</strong>、 <strong>From</strong>、 <strong>Received</strong>及<strong>Content-Type</strong>。官方的標頭欄位定義於 RFC 5322。非公務標頭欄位開頭<strong>X-</strong>和稱為<em>X 標頭</em>。</p></td>
</tr>
<tr class="odd">
<td><p><code>NotificationMessageText</code></p></td>
<td><p>純文字、 HTML 標籤和關鍵字的任意組合</p></td>
<td><p>指定要在收件者的通知訊息中使用的文字。</p>
<p>除了純文字與 HTML 標籤，您可以指定下列關鍵字使用值從原始郵件的：</p>
<ul>
<li><p><code>%%From%%</code></p></li>
<li><p><code>%%To%%</code></p></li>
<li><p><code>%%Cc%%</code></p></li>
<li><p><code>%%Subject%%</code></p></li>
<li><p><code>%%Headers%%</code></p></li>
<li><p><code>%%MessageDate%%</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>NotifySenderType</code></p></td>
<td><p>下列其中一個值：</p>
<ul>
<li><p><strong>通知寄件者，但允許他們傳送</strong>(<code>NotifyOnly</code>)</p></li>
<li><p><strong>封鎖郵件</strong>(<code>RejectMessage</code>)</p></li>
<li><p><strong>除非誤判封鎖郵件</strong>(<code>RejectUnlessFalsePositiveOverride</code>)</p></li>
<li><p><strong>封鎖郵件，但允許寄件者覆寫及傳送</strong>(<code>RejectUnlessSilentOverride</code>)</p></li>
<li><p><strong>封鎖郵件，但允許寄件者與業務上理由覆寫及傳送</strong>(<code>RejectUnlessExplicitOverride</code>)</p></li>
</ul></td>
<td><p>會指定原則提示寄件者會收到如果郵件違反 DLP 原則的類型。下列清單說明設定：</p>
<ul>
<li><p><strong>通知寄件者，但允許他們傳送</strong> 寄件者會收到通知，但郵件如常傳遞。</p></li>
<li><p><strong>封鎖郵件</strong> 郵件遭拒，並通知寄件者。</p></li>
<li><p><strong>除非誤判封鎖郵件</strong> 郵件遭拒，除非寄件者標示為誤判。</p></li>
<li><p><strong>封鎖郵件，但允許寄件者覆寫及傳送</strong> 郵件遭拒，除非寄件者選擇覆寫原則限制。</p></li>
<li><p><strong>封鎖郵件，但允許寄件者與業務上理由覆寫及傳送</strong> 已<strong>封鎖郵件，但允許寄件者覆寫及傳送</strong>類型類似，但是寄件者也可提供論證來覆寫原則限制。</p></li>
</ul>
<p>當您使用此巨集指令時，您需要使用此<strong>郵件包含敏感資訊</strong>(<em>MessageContainsDataClassification</em>) 條件。</p></td>
</tr>
<tr class="odd">
<td><p><code>RMSTemplate</code></p></td>
<td><p>單一 RMS template 物件</p></td>
<td><p>指定套用至郵件的 Rights Management Services (RMS) 範本。</p>
<p>在 EAC 中，您從清單中選取的 RMS 範本。</p>
<p>在Exchange 管理命令介面中，使用<strong>Get-RMSTemplate</strong>指令程式來查看可用的 RMS 範本。</p>
<p>RMS 需要Exchange企業用戶端存取授權 (Cal) 的每個信箱。如需 Cal 的詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 授權</a>。</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>下列其中一個值：</p>
<ul>
<li><p><strong>略過垃圾郵件篩選</strong>(<code>-1</code>)</p></li>
<li><p>整數 0 到 9</p></li>
</ul></td>
<td><p>會指定指派給郵件的垃圾郵件信賴等級 (SCL)。較高的 SCL 值表示郵件更多可能是垃圾郵件。</p></td>
</tr>
<tr class="odd">
<td><p><code>String</code></p></td>
<td><p>單一字串</p></td>
<td><p>會指定套用至指定的郵件標頭欄位、 NDR 或事件記錄檔項目的文字。</p>
<p>中Exchange 管理命令介面中，如果值包含空格，以引號 （&quot;） 括住值。</p></td>
</tr>
</tbody>
</table>


返回頁首

## 相關資訊

[管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[郵件流程規則動作在 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj919237\(v=exchg.150\)) 對於Exchange Online

Exchange Online Protection 的[郵件流程規則動作在 Exchange Online Protection](https://technet.microsoft.com/zh-tw/library/jj920117\(v=exchg.150\))

[整個組織的郵件免責聲明、 簽章、 頁尾或 Office 365 中的標頭](https://technet.microsoft.com/zh-tw/library/dn600323\(v=exchg.150\))

