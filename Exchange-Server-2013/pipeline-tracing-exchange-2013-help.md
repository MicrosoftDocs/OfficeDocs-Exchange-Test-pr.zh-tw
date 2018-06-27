---
title: '管線追蹤: Exchange 2013 Help'
TOCTitle: 管線追蹤
ms:assetid: e7780499-9a6f-48b1-aea8-df88ecd8b18a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125018(v=EXCHG.150)
ms:contentKeyID: 52062597
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管線追蹤

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

管線追蹤擷取從特定的寄件者的電子郵件訊息複本時移動透過信箱伺服器上，在 Mailbox server 上 Mailbox Transport 傳遞服務的傳輸服務以及透過 Edge Transport server.管線追蹤擷取每個傳輸代理程式套用至郵件的郵件快照檔案傳輸管線中變更的詳細資訊。檢查郵件快照檔案的內容，您可以決定傳輸代理程式是否已套用變更您所預期傳輸管線中的訊息。如果您疑難排解問題，您應該決定其傳輸代理程式是在容錯。然後您可以將您疑難排解的努力聚焦以解決問題的代理程式。然後您可以檢視再來確認您的解決方案已成功郵件快照檔案。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>管線追蹤複製完成從寄件者的電子郵件地址寄出的電子郵件的內容。若要避免不必要的機密資訊洩露，您需要設定適當的安全性權限的管線追蹤資料夾。</p></li>
<li><p>未啟用管線追蹤長的時間期間。管線追蹤會建立可以快速累積的檔案。永遠監視的可用磁碟空間時啟用管線追蹤。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 設定管線追蹤

啟用管線追蹤之前，您必須指定您想要監視的寄件者的電子郵件地址。管線追蹤的設計記錄從特定電子郵件地址傳送的訊息。至 Exchange 組織可以內部或外部寄件者的電子郵件地址。或者，您可以啟用指定信箱或邊際傳輸伺服器，例如自動回覆、 傳遞狀態通知 (DSN) 郵件、 日誌報告及其他系統產生的郵件您也可以修改的管線追蹤資料夾位置上的傳輸服務所產生的系統訊息的管線追蹤。

下表中已彙總您用來設定管線追蹤的參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>指令程式</th>
<th>參數</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingSenderAddress</em></p></td>
<td><p>空白 (<code>$null</code>)</p></td>
<td><p>指定您要監視之寄件者的電子郵件地址。</p>
<p>指定值 &quot;&lt;&gt;&quot; 來監視由伺服器上指定傳輸服務傳送之系統產生的郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingPath</em></p></td>
<td><p><strong>傳輸服務</strong>   <code>%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing</code></p>
<p><strong>信箱傳輸服務</strong>   <code>%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing</code></p></td>
<td><p>路徑必須是本機伺服器上。不支援 UNC 路徑。</p>
<p>指定路徑中包含管線追蹤檔案存放所在的 <code>MessageSnapshots</code> 資料夾。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingEnabled</em></p></td>
<td><p><code>$false</code></p></td>
<td><p>在您設定想要監視的寄件者地址之後，就只能對伺服器上指定的傳輸服務啟用管線追蹤。</p></td>
</tr>
</tbody>
</table>


如需如何啟用管線追蹤以及設定寄件者地址以進行管線追蹤的相關資訊，請參閱[設定管線追蹤](configure-pipeline-tracing-exchange-2013-help.md)。

## 郵件快照檔案

郵件快照集所需要擷取對一則訊息中的傳輸服務或信箱傳輸傳遞服務傳輸代理程式所做的任何變更的檔案。這些檔案儲存在`MessageSnapshots`資料夾中的傳輸服務的相對應管線追蹤路徑。

在`MessageSnapshots`資料夾中 Exchange 會建立一個針對每個受監視的寄件者通過指定之的傳輸服務所傳送的郵件資料夾。每個資料夾命名為後指定給郵件的 GUID。如果您啟用的傳輸服務與相同的信箱伺服器上的信箱傳輸服務的管線追蹤，不同的 GUID 指派給相同訊息的每個傳輸服務，所以的傳輸服務`MessageSnapshots`資料夾中的郵件\] 資料夾名稱是不同於相同的訊息中的信箱傳輸服務的`MessageSnapshots`資料夾的資料夾名稱。如果您啟用管線追蹤多個 Exchange 伺服器上的，它經過每一部 Exchange 伺服器上的指定之的傳輸服務指派不同的 GUID 相同的訊息。

每個郵件\] 資料夾中 Exchange 會建立具有.eml 副檔名的數個郵件快照檔案。這些郵件快照檔案包含郵件的內容如遇到每個 SMTP 事件和傳輸代理程式。

如果傳輸代理程式登錄在 SMTP 事件，Exchange 會建立郵件快照郵件的郵件遇到任何傳輸代理程式之前。這可讓您郵件的副本之前郵件遇到傳輸代理程式登錄該事件。接著，新郵件的快照集建立的每個傳輸代理程式的郵件遇到，不論是否傳輸代理程式會修改郵件的內容。不過，如果沒有代理程式登錄事件、 Exchange 不會建立該事件的任何郵件快照集。

例如，如果三個代理程式登錄**OnEndofData**事件，但只有兩個傳輸代理程式會修改一則訊息，所建立四個郵件的快照。第一個郵件快照擷取郵件為遇到**OnEndofData**事件之前該事件註冊傳輸代理程式所進行的任何修改。接著，不論是否傳輸代理程式會修改郵件每一個傳輸代理程式建立一個郵件快照。

下列清單中會描述已建立的郵件快照檔案：

  - **Original.eml**   在電子郵件發現任何 SMTP 事件或傳輸代理程式之前，此檔案包含該電子郵件的原始未修改內容。

  - **Routingnnnn.eml**這些檔案包含電子郵件的內容如遇到傳輸 SMTP 事件及傳輸代理程式上的傳輸服務的分類部分中的這些事件。版面配置區*nnnn*代表`0001`開頭的整數值。此值會遞增註冊這些事件的事件及代理程式的郵件處理的順序在每個 SMTP 事件和傳輸代理程式。Mailbox Transport 傳遞服務不會產生這些**Routing**快照檔案。

  - **SmtpReceivennnn.eml**這些檔案包含電子郵件的內容如遇到**OnEndofData**和**OnEndOfHeaders** SMTP 事件及傳輸代理程式登錄在這些事件期間 SMTP 接收的傳輸服務或信箱傳輸傳遞服務的一部分。版面配置區*nnnn*代表`0001`開頭的整數值。此值會遞增註冊這些事件的事件及代理程式的郵件處理的順序在每個 SMTP 事件和傳輸代理程式。

您可以使用記事本或任何文字編輯器來開啟郵件快照檔案。

每個郵件快照檔案開頭新增至訊息內容及列出郵件快照檔案與 SMTP 事件和傳輸代理程式標頭。這些標頭`X-CreatedBy: MessageSnapshot-Begin injected headers`的開頭和結尾`X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers`。這些標頭所取代每個後續傳輸代理程式及 SMTP 事件中每個郵件快照檔案。以下是會新增至電子郵件訊息檔標頭的範例：

    X-CreatedBy: MessageSnapshot-Begin injected headers
    X-MessageSnapshot-UTC-Time: 2013-01-23T23:20:18.138Z
    X-MessageSnapshot-Record-Id: 21474836486
    X-MessageSnapshot-Source: OnSubmittedMessageX-Sender: michelle@nwtraders.com
    X-Receiver: chris@contoso.com
    X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers

郵件的快照標頭之後, 的檔案包含包括所有原始的郵件標頭郵件的內容。如果傳輸代理程式會修改郵件的內容，所做的變更會出現訊息整合。當郵件處理每個傳輸代理程式中，每個代理程式所做的變更會套用至訊息內容。如果傳輸代理程式對訊息內容不進行任何變更，該代理程式所建立郵件快照將會與上一個傳輸代理程式所建立郵件快照相同。

