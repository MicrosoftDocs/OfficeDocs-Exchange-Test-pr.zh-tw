---
title: '郵件節流: Exchange 2013 Help'
TOCTitle: 郵件節流
ms:assetid: fba87902-2a79-42ac-b394-46a9016f667e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232205(v=EXCHG.150)
ms:contentKeyID: 50474645
ms.date: 01/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 郵件節流

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

*郵件節流*指的是在可由 Microsoft Exchange Server 2013 電腦處理的郵件和連線數目上，所設定的限制群組。這些限制能避免 Exchange 伺服器上的系統資源發生意外或蓄意的耗盡。

**目錄**

郵件節流範圍

郵件成本和郵件流程節流

伺服器上的郵件節流

傳送連接器上的郵件節流

接收連接器上的郵件節流

郵件節流原則

## 郵件節流範圍

郵件節流牽涉到許多對於郵件處理速率、SMTP 連線速率以及 SMTP 工作階段逾時值等限制。將這些限制合併使用，可以保護 Exchange 伺服器以免因接受和傳遞郵件而負擔過重。儘管可能有大量待處理的郵件和連線在等著處理，郵件節流限制讓 Exchange 伺服器能夠以有條理的方式處理郵件和連線。

除了郵件節流之外，您也可以對郵件的個別元件加上大小限制，例如收件者數目、郵件標頭的大小，或是個別附件的大小。如需郵件大小限制的相關資訊，請參閱[郵件大小限制](message-size-limits-exchange-2013-help.md)。

另一項幫助避免 Exchange 傳輸伺服器上系統資源不堪負荷的功能是*背壓*。背壓是信箱伺服器和 Edge Transport Server 上，傳輸服務中的系統資源監視功能。如果受監視的系統資源 (例如硬碟使用量或記憶體使用量) 超過指定的閾值，伺服器就會減少接受新的連線及郵件率，並專注傳遞現有的郵件。當受監視的系統資源之使用情況回到正常層級，伺服器會緩慢增加其速度，直到它接受新的連線，然後恢復到正常層級。

回到頁首

## 郵件成本和郵件流程節流

為提供更一致的郵件輸送量與可預測的郵件傳遞延遲，Exchange 2013 建立了一項郵件的累計成本。此服務品質 (QoS) 功能已加入至 Microsoft Exchange Server 2010 SP1。此成本是根據下列準則：

  - 郵件大小

  - 收件者數目

  - 傳輸頻率

Exchange 2013 傳輸伺服器會追蹤個別使用者傳送之郵件的平均傳遞成本。藉由使用郵件成本，Exchange 2013 提供了一組設定，能用來控制 Exchange 組織中某個使用者或連線所造成的影響。此組設定稱為*節流原則*。當某個使用者重複地寄送耗費成本的郵件 (例如含有大型附件或寄送給多位收件者的郵件) 時，採用 Exchange 2013 的傳輸伺服器將會使用節流原則，將該使用者所寄送的較高成本郵件指派為較低的優先順序，同時又持續傳遞較低成本的郵件。這項新行為可增加 Exchange 2013 中郵件節流功能的「服務品質」部分。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>從使用者觀點來看，郵件節流並不會影響郵件優先順序。郵件將持續保有使用者所設定的原先優先順序。例如，郵件將保有「重要」或「緊急」等設定。</td>
</tr>
</tbody>
</table>


為了支援此功能，Exchange 2013 採用以下的機制：

  - **內部優先順序代理程式**   這個代理程式將於 **OnResolvedMessage** 事件中觸發，並指派較低的優先順序給來自擁有高累計成本的相同寄件者之郵件。此成本之衡量是以一分鐘的週期來計算，並且將影響到擁有超過 500 個收件者，或是大小超過 1 MB 之郵件。

  - **適用於 MapiDelivery 佇列類型的配額式優先順序佇列**   這個機制會讓 Exchange 以正常優先順序佇列傳遞郵件，其頻率將比低優先順序佇列的郵件還高。依據預設，正常與低郵件之比率為 20：1。然而，來自較低優先順序佇列之新郵件的傳遞，絕不會快於來自較高優先順序佇列之新物件。例如，請考量下列情境：
    
    1.  已傳遞二十封正常優先順序之郵件。依據預設，下一個傳送的郵件為較低優先順序之郵件。
    
    2.  傳輸伺服器收到兩封新郵件：一封郵件來自較高優先順序佇列，一封郵件來自較低優先順序佇列。
    
    在此情境中，來自較高優先順序佇列的郵件將優先傳遞。接著再傳遞來自較低優先順序之郵件。

  - **依據郵件傳遞資料庫健康狀況調節同時連線數**   此機制將監視 Exchange 郵件傳遞資料庫 (MDB) 之健康狀況，並根據所指定的健康狀況量值對 Exchange 傳輸伺服器的同時連線數進行調節。MDB 是由郵件伺服器上傳輸服務中的 Resource Health Monitor API 進行監視，並指派了自 -1 至 100 的健康值。這個數值是以 RPC 效能統計資料為依據，該資料附於信箱傳輸服務之 Store.exe 程序的每個 RPC 回應之中。Resource Health 架構使用了 **Requests/Second** 率之效率計數器與 **Average RPC Latency** 效能計數器來計算資料庫之健康值。為協助維持一致的互動性使用者體驗，Exchange 會隨著健康值降低而減少同時連線的數目。可用的健康值範圍如下：
    
      - **-1：**這個值表示 MDB 健康狀態為未知。當資料庫啟動時會指派此數值。在此情況下，會將資料庫視為健康。
    
      - **0：**如果資料庫處於不健康的狀態，會指派此數值。在此狀態下，不應連接該資料庫。
    
      - **1 至 99：**這些數值代表了一般的健康狀態。較低的值表示健康狀態較差的資料庫。
    
      - **100：**這個值代表健康良好的資料庫。

Microsoft Exchange 節流服務為郵件流程節流提供了框架。Microsoft Exchange 節流服務能持續追蹤某特定使用者的郵件流程節流設定，並將節流資訊儲存於記憶體中。郵件流程節流設定也稱為*預算*。重新啟動 Microsoft Exchange 節流服務也會重設郵件流程節流預算。

您可以使用 Exchange 2013 所提供的節流原則 Cmdlet，為某個節流原則設定個別的預算設定。預算的定義為某個使用者或應用程式在某特定設定中所擁有的存取數量。預算代表了使用者所能擁有的連線數目、或使用者在每一分鐘的期間內所被允許的活動數目。例如，可透過設定預算，來設定某個使用者在 Exchange (如 ActiveSync、Outlook Web App 或 Exchange Web 服務) 中所能使用的時間長度。此閥值會儲存於節流原則中並定義預算。

預算的時間設定會以一分鐘的百分比例來進行設定。因此，100% 的閾值便代表 60 秒。例如，假設您想要指定 Outlook Web App 原則設定，將使用者在用戶端存取伺服器上執行 Outlook Web App 碼期間中的時間與該使用者與用戶端存取進行通訊的時間，限制在每一分鐘的期間內為 600 毫秒。為達成此目的，您必須將以下兩個參數之數值設定為一分鐘 (600 毫秒) 的 1%：

  - **OWAPercentTimeInCAS：**1

  - **OWAPercentTimeInMailboxRPC：**1

套用此原則的使用者，便擁有 600 毫秒 OWAPercentTimeInCAS 與 600豪秒 OWAPercentageTimeInMailboxRPC 之預算。在此情況中，當使用者登入 Outlook Web App 時，該使用者能夠執行用戶端存取碼長達 600 毫秒。在 600 毫秒之後，該連線便被認為超出預算，因此 Exchange 伺服器便不再允許更多的 Outlook Web App 動作，直到達到預算限制後經過一分鐘後為止。經過一分鐘之後，使用者又能執行 Outlook Web App 用戶端存取碼長達 600 毫秒。

回到頁首

## 伺服器上的郵件節流

您可以設定下列位置的郵件節流選項：

  - 在傳輸服務中

  - 在傳送連接器上

  - 在接收連接器上

您可以在信箱伺服器上的傳輸服務、信箱伺服器上的信箱傳輸服務，或用戶端存取伺服器上的前端傳輸服務中，設定所有可用的郵件節流選項。您也可以在 Exchange 系統管理中心 (EAC) 中設定傳輸伺服器內容，以便設定部分相同選項。

下表顯示可用於傳輸伺服器的郵件節流選項。

### 傳輸伺服器上的郵件節流選項

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>來源</th>
<th>參數</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxDeliveries</em></p></td>
<td><p>20</p></td>
<td><p>此參數指定傳輸服務同時開啟以將郵件傳遞至信箱的傳遞執行緒數上限。此參數的有效輸入範圍是 1 到 256。除非是 Microsoft 客戶服務與支援中心的建議，否則建議您不要修改預設值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxSubmissions</em></p></td>
<td><p>20</p></td>
<td><p>此參數指定傳輸服務同時開啟以從信箱傳送郵件的提交執行緒數上限。此參數的有效輸入範圍是 1 到 256。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MaxConnectionRatePerMinute</em></p></td>
<td><p>1200</p></td>
<td><p>此參數指定允許開啟的傳輸服務連線率上限。如果同時發生傳輸服務的多個連線嘗試，則 <em>MaxConnectionRatePerMinute</em> 參數會限制開啟的連線率，這樣伺服器的資源才不會過度忙碌。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong> 或</p>
<p>傳輸伺服器內容</p></td>
<td><p><em>MaxOutboundConnections</em></p></td>
<td><p>1000</p></td>
<td><p>此參數指定一次可開啟的輸出連線數目上限。如果輸入 <code>unlimited</code> 值，則不會限制輸出連線數目。參數的值必須大於或等於 <em>MaxPerDomainOutboundConnections</em> 參數的值。</p>
<p>也可利用 [伺服器] &gt; [伺服器] &gt; [內容] &gt; [傳輸限制] &gt; [輸出連線限制] 設定該值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> 或</p>
<p>傳輸伺服器內容</p></td>
<td><p><em>MaxPerDomainOutboundConnections</em></p></td>
<td><p>20</p></td>
<td><p>此參數指定可連至任何單一網域的同時連線數目上限。如果輸入 <code>unlimited</code> 值，則不會限制每個網域的輸出連線數目。參數的值必須大於或等於 <em>MaxOutboundConnections</em> 參數的值。</p>
<p>也可利用 [伺服器] &gt; [伺服器] &gt; [內容] &gt; [傳輸限制] &gt; [輸出連線限制] 設定該值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>PickupDirectoryMaxMessagesPerMinute</em></p></td>
<td><p>100</p></td>
<td><p>此參數指定收取目錄及重新顯示目錄每分鐘要處理的郵件數目上限。每個目錄可使用此參數所指定的速率，獨立處理郵件檔案。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 傳送連接器上的郵件節流

下表顯示可用於傳送連接器的郵件節流選項。您必須使用 Exchange 管理命令介面，來設定此選項。

### 傳送連接器上可用的郵件節流選項

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>來源</th>
<th>參數</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-SendConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10 分鐘</p></td>
<td><p>此參數指定在關閉連線之前，與目的郵件伺服器的開啟 SMTP 連線可以持續閒置的時間上限。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 接收連接器上的郵件節流

下表顯示可供信箱伺服器或 Edge Transport Server 上傳輸服務中設定之接收連接器使用的郵件節流選項。您必須使用 Exchange 管理命令介面，來設定這些選項。

### 接收連接器上可用的郵件節流選項

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>來源</th>
<th>參數</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>在郵件伺服器上傳輸服務的 5 分鐘</p>
<p>在用戶端存取伺服器上前端傳輸服務的 5 分鐘。</p>
<p>邊際傳輸伺服器上的 1 分鐘。</p></td>
<td><p>此參數指定在關閉連線之前，與來源郵件伺服器的開啟 SMTP 連線可以持續閒置的時間上限。此參數的值需小於由 <em>ConnectionTimeout</em> 參數指定的值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionTimeOut</em></p></td>
<td><p>在郵件伺服器上傳輸服務的 10 分鐘</p>
<p>在用戶端存取伺服器上前端傳輸服務的 10 分鐘。</p>
<p>邊際傳輸伺服器上的 5 分鐘。</p></td>
<td><p>此參數指定與來源郵件伺服器的 SMTP 連線可以持續開啟的時間上限 (即使來源郵件伺服器正在傳輸資料)。此參數的值需大於由 <em>ConnectionInactivityTimeout</em> 參數指定的值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnection</em></p></td>
<td><p>5000</p></td>
<td><p>此參數指定此接收連接器同時間允許的輸入 SMTP 連線數目上限。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPercentagePerSource</em></p></td>
<td><p>信箱伺服器上之傳輸服務中的預設接收連接器為 100%</p>
<p>信箱伺服器上之傳輸服務，以及用戶端存取伺服器上之前端傳輸服務中的其他接收連接器為 2%。</p></td>
<td><p>此參數可指定接收連接器同時允許來自單一來源郵件伺服器的 SMTP 連線數目上限。此值是以接收連接器上可用的其餘連線百分比來表示。<em>MaxInboundConnection</em> 參數定義了接收連接器所允許的連線數目上限。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPerSource</em></p></td>
<td><p>信箱伺服器上之傳輸服務中的預設接收連接器為 unlimited</p>
<p>信箱伺服器上之傳輸服務，以及用戶端存取伺服器上之前端傳輸服務中的其他接收連接器為 20。</p></td>
<td><p>此參數可指定接收連接器同時允許來自單一來源郵件伺服器的 SMTP 連線數目上限。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxProtocolErrors</em></p></td>
<td><p>5</p></td>
<td><p>此參數指定接收連接器在關閉與來源郵件伺服器的連線之前，所允許的 SMTP 通訊協定錯誤數目上限。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>TarpitInterval</em></p></td>
<td><p>5 秒</p></td>
<td><p>此參數指定用於<em>「垃圾郵件防堵」</em>的延遲。「垃圾郵件防堵」是指針對指出目錄搜尋攻擊或其他擾人郵件的特定 SMTP 通訊模式，以人工方式延遲 SMTP 回應的作法。<em>「目錄搜集攻擊」</em>會嘗試從特定組織收集有效的電子郵件地址，以用作未經同意的廣告郵件目標。</p>
<p><em>TarpitInterval</em> 參數所指定的延遲只適用於匿名連線。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 郵件節流原則

在 Exchange 2013 中，每個信箱都有 *ThrottlingPolicy* 設定。此設定的預設值為空白 (`$null`)。您可以在 **Set-Mailbox** Cmdlet 上使用 *ThrottlingPolicy* 參數，用以設定信箱的節流原則。

對於連線至 Exchange 的使用者，已存在預設的節流原則，以提供預設的預算設定。若要替一位以上的使用者設定自訂預算設定，請建立新的節流原則。接著將該原則套用至適用的使用者或群組上。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您不要修改預設的節流原則。</td>
</tr>
</tbody>
</table>


您可以在 Exchange 管理命令介面中，設定信箱伺服器上可用的所有郵件節流選項。下列指令程式可供您管理節流原則：

  - **Get-ThrottlingPolicy**

  - **Remove-ThrottlingPolicy**

  - **New-ThrottlingPolicy**

  - **Set-ThrottlingPolicy**

您可以使用 **New-ThrottlingPolicy** 與 **Set-ThrottlingPolicy** Cmdlet，設定一名使用者在某特定連線或期間內於 Exchange 所能進行的活動量。這些設定構成了使用者的預算。您可以建立節流原則，以控制對下列 Exchange 功能之存取：

  - Exchange ActiveSync

  - Exchange Web 服務

  - Outlook Web App

  - 整合通訊

  - IMAP4

  - POP3

  - Outlook 用戶端連線 (MAPI 或 RPC 連線)

  - 郵件流程設定

  - PowerShell 命令

  - CPU 使用量

回到頁首

