---
title: '郵件大小限制: Exchange 2013 Help'
TOCTitle: 郵件大小限制
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 50474037
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 郵件大小限制

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-08-20_

您可以將限制套用至在 Microsoft Exchange Server 2013 組織之間移動的個別郵件。您可以限制郵件的總大小或郵件個別元件的大小，例如郵件標頭、郵件附件和收件者數目。您可以對整個 Exchange 組織全面套用限制，或特別針對連接器或使用者物件套用限制。

在規劃 Exchange 組織的郵件大小限制時，請考慮下列問題：

  - 我應該對所有內送郵件加上何種大小限制？

  - 我應該對所有外寄郵件加上何種大小限制？

  - Exchange 組織的信箱配額為何？

  - 我選擇的郵件大小限制會如何影響信箱配額大小？

  - 我的 Exchange 組織內是否有一些使用者必須傳送或接收大於所指定允許大小的郵件？

  - 我的 Exchange 網路拓撲是否包含其他具有不同郵件大小限制的郵件系統或個別業務單位？

本主題提供的指導可協助您回答這些問題。

**目錄**

郵件大小限制類型

限制的範圍

郵件大小限制的優先順序

不受大小限制的郵件

## 郵件大小限制類型

以下是適用於個別郵件的大小上限基本類別：

  - **郵件標頭大小限制** 這些限制適用於郵件中所有郵件標頭欄位的總大小。郵件內文或附件的大小不考慮在內。因為標頭欄位是純文字，所以標頭大小是由每個標頭欄位中的字元數以及標頭欄位的總數來決定。文字中的每個字元都佔用 1 個位元組。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>部分協力廠商防火牆或 Proxy 伺服器會套用它們自己的郵件標頭大小限制。這些協力廠商防火牆或 Proxy 伺服器可能會無法處理附件檔名稱超過 50 個字元的郵件，或附件檔名稱包含非 US-ASCII 字元的郵件。</td>
    </tr>
    </tbody>
    </table>


  - **郵件大小限制**   這些限制適用於郵件的總大小，其中包括郵件標頭、郵件內文和任何附件。郵件大小限制可套用至內送郵件或外寄郵件。執行內部郵件流程時，Exchange 會使用自訂 `X-MS-Exchange-Organization-OriginalSize:` 郵件標頭來記錄郵件進入 Exchange 組織時的原始郵件大小。每當以指定的郵件大小限制來檢查郵件時，會使用目前郵件大小或原始郵件大小標頭兩者中的較低值。郵件大小可能因為內容轉換、編碼和代理程式處理而變更。

  - **附件大小限制** 這些限制適用於郵件內允許的單一附件大小上限。郵件可能會包含許多大幅增加郵件整體大小的附件。不過，附件大小限制只會套用至個別附件的大小。

  - **收件者限制** 這些限制適用於郵件收件者的總數。剛開始撰寫郵件時，收件者存在於 `To:`、`Cc:` 及 `Bcc:` 標頭欄位中。當提交郵件進行傳遞時，郵件收件者會轉換成郵件信封中的 `RCPT TO:` 項目。在郵件提交期間，通訊群組會以單一收件者計算。

回到頁首

## 限制的範圍

以下是適用於個別郵件的限制範圍基本類別：

  - **組織限制**   這些限制適用於組織內所有的 Exchange 2013 信箱伺服器以及 Exchange 2010 和 Exchange 2007 Hub Transport Server。如果您的周邊網路中已安裝 Edge Transport Server，則指定的限制會套用到特定伺服器。

  - **連接器限制**   這些限制適用於使用指定的傳送連接器、接收連接器、傳遞代理程式連接器或外部連接器進行郵件傳遞的任何郵件。傳送連接器是在信箱伺服器和 Edge Transport Server 上的傳輸服務中定義。接收連接器是在信箱伺服器上的傳輸服務、用戶端存取伺服器上的前端傳輸服務，以及 Edge Transport Server 上定義。

  - **Active Directory 站台連結**   信箱伺服器上的傳輸服務會使用 Active Directory 站台以及指派給 Active Directory IP 站台連結的成本做為其中一個因素，判斷組織內信箱伺服器之間成本最低的路由傳送路徑。您可以將特定郵件大小限制指派給組織中的 Active Directory 站台連結。

  - **伺服器限制**   這些限制適用於特定信箱伺服器或 Edge Transport Server。您可以在每一部信箱伺服器或 Edge Transport Server 上獨立地設定指定的郵件限制。
    
    在 Outlook Web App 中，用戶端存取伺服器上的 HTTP 要求大小上限設定也會控制 Outlook Web App 使用者可傳送的郵件大小。

  - **使用者限制**   這些限制適用於特定的使用者物件，例如信箱、連絡人、通訊群組或公用資料夾。

下表說明郵件限制，包括有關如何在 Exchange 管理命令介面或 Exchange 系統管理中心 (EAC) 中設定限制的資訊。

### 組織限制

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>大小限制</th>
<th>預設值</th>
<th>命令介面組態</th>
<th>EAC 組態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>接收的郵件大小上限</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet：<strong>Set-TransportConfig</strong></p>
<p>參數：<em>MaxReceiveSize</em></p></td>
<td><p><strong>郵件流程</strong> &gt; <strong>接收連接器</strong> &gt; <strong>更多選項</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多選項圖示" alt="更多選項圖示" /> &gt; <strong>組織傳輸設定</strong> &gt; <strong>限制</strong>索引標籤 &gt; <strong>接收郵件大小上限</strong></p></td>
</tr>
<tr class="even">
<td><p>傳送的郵件大小上限</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet：<strong>Set-TransportConfig</strong></p>
<p>參數：<em>MaxSendSize</em></p></td>
<td><p><strong>郵件流程</strong> &gt; <strong>接收連接器</strong> &gt; <strong>更多選項</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多選項圖示" alt="更多選項圖示" /> &gt; <strong>組織傳輸設定</strong> &gt; <strong>限制</strong>索引標籤 &gt; <strong>傳送郵件大小上限</strong></p></td>
</tr>
<tr class="odd">
<td><p>每封郵件的收件者數目上限</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
</tr>
</tbody>
</table>

</td>
<td><p>5000</p></td>
<td><p>Cmdlet：<strong>Set-TransportConfig</strong></p>
<p>參數：<em>MaxRecipientEnvelopeLimit</em></p></td>
<td><p><strong>郵件流程</strong> &gt; <strong>接收連接器</strong> &gt; <strong>更多選項</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多選項圖示" alt="更多選項圖示" /> &gt; <strong>組織傳輸設定</strong> &gt; <strong>限制</strong>索引標籤 &gt; <strong>收件者數目上限</strong></p></td>
</tr>
<tr class="even">
<td><p>套用至組織中所有信箱伺服器的傳輸規則之附件大小上限</p></td>
<td><p>未設定</p></td>
<td><p>Cmdlet：<strong>New-TransportRule</strong>、<strong>Set-TransportRule</strong></p>
<p>參數：<em>AttachmentSizeOver</em></p></td>
<td><p><strong>郵件流程</strong> &gt; <strong>規則</strong> &gt; <strong>新增</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="加入圖示" alt="加入圖示" /> 或<strong>編輯</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" />。</p>
<p>使用述詞<strong>若為以下情況，套用這個規則</strong> &gt; <strong>任何附件</strong> &gt; <strong>大於或等於</strong></p>
<p>使用述詞<strong>若為以下情況，套用這個規則</strong> &gt; <strong>訊息</strong> &gt; <strong>大小大於或等於</strong></p></td>
</tr>
<tr class="odd">
<td><p>套用至組織中所有信箱伺服器的傳輸規則之郵件大小上限</p></td>
<td><p></p></td>
<td><p>Cmdlet：<strong>New-TransportRule</strong>、<strong>Set-TransportRule</strong></p>
<p>參數：<em>MessageSizeOver</em></p></td>
<td><p><strong>郵件流程</strong> &gt; <strong>規則</strong> &gt; <strong>新增</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="加入圖示" alt="加入圖示" /> 或<strong>編輯</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" />。</p>
<p>使用述詞<strong>若為以下情況，套用這個規則</strong> &gt; <strong>訊息</strong> &gt; <strong>大小大於或等於</strong></p></td>
</tr>
</tbody>
</table>


回到頁首

### 連接器限制

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>大小限制</th>
<th>預設值</th>
<th>命令介面組態</th>
<th>EAC 組態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>透過接收連接器的標頭大小上限</p></td>
<td><p>128 KB</p></td>
<td><p>Cmdlet：<strong>New-ReceiveConnector</strong>、<strong>Set-ReceiveConnector</strong></p>
<p>參數：<em>MaxHeaderSize</em></p></td>
<td><p>無</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>透過接收連接器的郵件大小上限</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>實際的郵件大小可能因為郵件編碼和內容轉換的關係而更小。</td>
</tr>
</tbody>
</table>

</td>
<td><p><strong>在 Mailbox Server 上的運輸服務</strong></p>
<p>預設和用戶端 Proxy 傳送連接器為 35 MB</p>
<p><strong>用戶端存取伺服器上的前端傳輸服務，即套用此規則</strong></p>
<p>預設前端和輸出 Proxy 前端接收連接器為 36 MB。</p>
<p>用戶端前端接收連接器為 35 MB。</p></td>
<td><p>Cmdlet：<strong>New-ReceiveConnector</strong>、<strong>Set-ReceiveConnector</strong></p>
<p>參數：<em>MaxMessageSize</em></p></td>
<td><p><strong>郵件流程</strong> &gt; <strong>接收連接器</strong> &gt; <strong>編輯</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" /> &gt; <strong>一般</strong>索引標籤 &gt; <strong>接收郵件大小上限</strong></p></td>
</tr>
<tr class="odd">
<td><p>透過接收連接器之每封郵件的收件者數目上限</p></td>
<td><p><strong>在 Mailbox Server 上的運輸服務</strong></p>
<p>預設接收連接器為 5,000</p>
<p>用戶端 Proxy 接收連接器為 200</p>
<p><strong>用戶端存取伺服器上的前端傳輸服務，即套用此規則</strong></p>
<p>預設前端、用戶端前端和用戶端 Proxy 前端接收連接器為 200。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果匿名寄件者所指定的收件者數目超過此值，則會讓前 200 位收件者收到郵件。大部分 SMTP 郵件伺服器會偵測到收件者限制。在將郵件傳遞給所有收件者之前，SMTP 郵件伺服器會繼續以 200 位收件者為單位來重送郵件。</td>
</tr>
</tbody>
</table>

</td>
<td><p>Cmdlet：<strong>New-ReceiveConnector</strong>、<strong>Set-ReceiveConnector</strong></p>
<p>參數：<em>MaxRecipientsPerMessage</em></p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>透過傳送連接器的郵件大小上限</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet：<strong>New-SendConnector</strong>、<strong>Set-SendConnector</strong></p>
<p>參數：<em>MaxMessageSize</em></p></td>
<td><p><strong>郵件流程</strong> &gt; <strong>傳送連接器</strong> &gt; <strong>編輯</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" /> &gt; <strong>一般</strong>索引標籤 &gt; <strong>傳送郵件大小上限</strong></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>透過 Active Directory 站台連結的郵件大小上限</p></td>
<td><p>無限制</p></td>
<td><p>Cmdlet：<strong>Set-AdSiteLink</strong></p>
<p>參數：<em>MaxMessageSize</em></p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>透過傳遞代理程式連接器的郵件大小上限</p></td>
<td><p>無限制</p></td>
<td><p>Cmdlet：<strong>New-DeliveryAgentConnector</strong>、<strong>Set-DeliveryAgentConnector</strong></p>
<p>參數：<em>MaxMessageSize</em></p></td>
<td><p>無</p></td>
</tr>
<tr class="odd">
<td><p>透過外部連接器的郵件大小上限</p></td>
<td><p>無限制</p></td>
<td><p><strong>Cmdlet: Set-ForeignConnector</strong> 參數：<em>MaxMessageSize</em></p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


回到頁首

### 伺服器限制

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>大小限制</th>
<th>預設值</th>
<th>命令介面組態</th>
<th>EAC 組態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>收取目錄中的郵件標頭大小上限</p></td>
<td><p>64 KB</p></td>
<td><p>Cmdlet：<strong>Set-TransportService</strong></p>
<p>參數：<em>PickupDirectoryMaxHeaderSize</em></p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>收取目錄中每封郵件的收件者數目上限</p></td>
<td><p>100</p></td>
<td><p>Cmdlet：<strong>Set-TransportService</strong></p>
<p>參數：<em>PickupDirectoryMaxRecipientsPerMessage</em></p></td>
<td><p>無</p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App、Exchange ActiveSync 與 Exchange Web 服務用戶端的用戶端特定郵件大小上限</p></td>
<td><p>Outlook Web App   35 MB</p>
<p>Exchange ActiveSync   10 MB</p>
<p>Exchange Web 服務   64 MB</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由於 Base64 編碼所產生的相關負荷，這些值會比實際可用的郵件大小上限多出約 33%。</td>
</tr>
</tbody>
</table>

</td>
<td><p>您可在 Client Access Server 上的適當 web.config XML 應用程式組態檔中設定這些值。如需詳細資訊，請參閱<a href="configure-client-specific-message-size-limits-exchange-2013-help.md">設定用戶端特定的郵件大小限制</a>。</p></td>
<td><p>無</p></td>
</tr>
</tbody>
</table>


回到頁首

### 使用者限制

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>大小限制</th>
<th>預設值</th>
<th>命令介面組態</th>
<th>EAC 組態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>可由此收件者傳送的郵件大小上限</p></td>
<td><p>無限制</p></td>
<td><p>Cmdlet：</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-RemoteMailbox</strong></p>
<p>參數：<em>MaxSendSize</em></p></td>
<td><p>對於信箱：</p>
<p><strong>收件者</strong> &gt; <strong>信箱</strong> &gt; <strong>編輯</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" /> &gt; <strong>信箱功能</strong> &gt; <strong>郵件流程</strong> &gt; <strong>郵件大小限制</strong> &gt; <strong>檢視詳細資料</strong> &gt; <strong>已傳送的郵件</strong></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用其他收件者類型的 EMC 進行此設定。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>可傳送至此收件者的郵件大小上限</p></td>
<td><p>無限制</p>
<p>針對站台信箱提供原則：36 MB</p></td>
<td><p>Cmdlet：</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>New-SiteMailboxProvisioningPolicy</strong></p>
<p><strong>Set-SiteMailboxProvisioningPolicy</strong></p>
<p>參數：<em>MaxReceiveSize</em></p></td>
<td><p>對於信箱：</p>
<p><strong>收件者</strong> &gt; <strong>信箱</strong> &gt; <strong>編輯</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" /> &gt; <strong>信箱功能</strong> &gt; <strong>郵件流程</strong> &gt; <strong>郵件大小限制</strong> &gt; <strong>檢視詳細資料</strong> &gt; <strong>已接收的郵件</strong></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用其他收件者類型的 EMC 進行此設定。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>由此收件者傳送之每封郵件的收件者數目上限</p></td>
<td><p>無限制</p></td>
<td><p>Cmdlet：</p>
<p><strong>Set-Mailbox</strong>, <strong>Set-MailUser</strong></p>
<p>參數：<em>RecipientLimits</em></p>
<p></p></td>
<td><p>無</p></td>
</tr>
</tbody>
</table>


回到頁首

## 郵件大小限制的優先順序

您可以在 Exchange 組織的不同層級上設定不同的郵件大小限制。由於郵件會透過您的傳輸基礎架構進行路由傳送，因此可能會受到數種不同郵件大小的限制。規劃郵件大小限制時，應確定傳輸管線中的郵件在違反郵件大小限制時能盡快遭到拒絕。一般來說，您應在郵件進入基礎架構的地點上設定更嚴格的限制。例如，在從網際網路接收郵件的接收連接器上，任何的郵件大小限制都應小於或等於您為內部 Exchange 組織所設定的郵件大小限制。如果 Exchange 伺服器從網際網路接收及處理的郵件遭到信箱伺服器上的傳輸服務拒絕，對於系統資源而言會是一種浪費。請確定您的組織、伺服器和連接器限制的設定可將任何不必要的郵件處理量降至最低。

此方法的其中一個例外是使用者限制。使用者層級限制的優先順序高於郵件大小限制。因此，您可以設定超過組織預設郵件大小限制的使用者。例如，您可以為這些信箱設定自訂的傳送和接收限制，以允許特定使用者信箱群組傳送比組織其他人更大的郵件。

使用者限制的例外情況，僅適用於經授權使用者間的郵件交流。若是一則郵件送到網際網路上的收件者，或是由其所接收，則將會套用組織限制。例如，假設您的組織郵件大小限制為 10 MB，但是您已將行銷部門內部的使用者設定為可接收與傳送最大 50 MB 的郵件。這些使用者將能夠在彼此間交流大型郵件，但仍將無法自網際網路使用者處接收大型郵件，因為這些郵件將來自於未經授權的寄件者。

回到頁首

## 不受大小限制的郵件

下列清單顯示信箱伺服器或 Edge Transport Server 所產生且不受所有郵件大小限制的郵件類型：

  - 系統郵件

  - 代理程式產生的郵件

  - 傳遞狀態通知 (DSN) 郵件

  - 日誌報告郵件

  - 隔離郵件

不過，這些郵件仍會受到郵件中收件者數目上限的組織值所限制。

回到頁首

