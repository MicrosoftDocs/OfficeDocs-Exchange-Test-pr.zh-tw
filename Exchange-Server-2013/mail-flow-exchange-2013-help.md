---
title: '郵件流程: Exchange 2013 Help'
TOCTitle: 郵件流程
ms:assetid: 14df5e1a-a5f7-4b0d-ba97-f53b76f0e7e0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996349(v=EXCHG.150)
ms:contentKeyID: 50472627
ms.date: 01/14/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 郵件流程

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

在 Microsoft Exchange Server 2013中，郵件流程會通過傳輸管線發生。\[傳輸管線\]* * 是服務、連線、元件及佇列的集合，這些項目會一起運作，將所有郵件路由傳送到組織內部之信箱伺服器上傳輸服務的分類程式。

尋找所有郵件流程主題的清單嗎？請參閱郵件流程文件。

如需如何在新的 Exchange 2013 組織中設定郵件流程的相關資訊，請參閱[設定郵件流程和用戶端存取](configure-mail-flow-and-client-access-exchange-2013-help.md)。

**目錄**

傳輸管線

在 Mailbox Server 上的運輸服務

郵件流程文件

## 傳輸管線

傳輸管線是由下列服務所組成：

  - **Client Access servers 上的前端傳輸服務**   此服務會作為 Exchange 2013 組織所有輸入和輸出 (選用) 的外部 SMTP 流量的無狀態 Proxy。前端傳輸服務不會檢查郵件內容、不會與信箱伺服器上的信箱傳輸服務通訊，且不會在本機將任何郵件排入佇列中。

  - **信箱伺服器上的傳輸服務**   此服務實際上等同於舊版 Exchange 中的 Hub Transport server role。傳輸服務處理所有組織的 SMTP 郵件流程，執行郵件分類，並執行郵件內容檢查。和舊版 Exchange 不同的是，Transport 服務不會直接和信箱資料庫進行通訊。這項工作現在是由 Mailbox Transport 服務來處理。傳輸服務會在信箱傳輸服務、傳輸服務、前端傳輸服務與 Edge Transport Server 上的傳輸服務 (視您的組態而定) 之間路由傳送郵件。信箱伺服器上的傳輸服務將在本主題的後續內容中詳細說明。

  - **信箱伺服器上的信箱傳輸服務**   此服務由兩項個別服務組成：Mailbox Transport Submission 服務和 Mailbox Transport Delivery 服務。信箱傳輸傳遞服務接收來自本機信箱伺服器或其他信箱伺服器上的 SMTP 郵件，並使用 Exchange 遠端程序呼叫 (RPC) 連接至本機信箱資料庫以傳送郵件。信箱傳輸提交服務將使用 RPC 連接至本機信箱資料庫以擷取郵件，並透過 SMTP 將郵件提交至本機信箱伺服器或信箱伺服器的傳輸服務。信箱傳輸提交服務可存取與傳輸服務相同的路由拓撲資訊。與前端傳輸服務類似，信箱傳輸服務也不會在本機佇列任何郵件。

  - **Edge Transport Server 上的傳輸服務**   此服務非常類似於信箱伺服器上的傳輸服務。如果您在周邊網路中安裝了 Edge Transport Server，所有來自網際網路或送出至網際網路的郵件，都將通過傳輸服務 Edge Transport Server。此服務將在本主題的後續內容中詳細說明。

下圖顯示 Exchange 2013 傳輸管線中元件之間的關係。

**Exchange 2013 傳輸管線概觀。**

![傳輸管線概觀圖表](images/Aa996349.6f548b64-6ac2-4e98-9098-69ad6cd9f569(EXCHG.150).gif "傳輸管線概觀圖表")

## 來自外部寄件者的郵件

來自組織以外的郵件會透過 Client Access Server 上的前端傳輸服務中的接收連接器進入傳輸管線，然後路由傳送至信箱伺服器上的傳輸服務。

如果您在周邊網路中安裝了 Exchange 2013 Edge Transport Server，則來自組織以外的郵件會透過 Edge Transport Server 上的傳輸服務中的接收連接器進入傳輸管線。郵件後續會送至何處，取決於您內部 Exchange 伺服器的設定方式。

  - **安裝在同一部電腦上的信箱伺服器和 Client Access Server**   在此組態中，輸入郵件流程會使用 Client Access Server。郵件會從 Edge Transport Server 上的傳輸服務流向 Client Access Server 上的前端傳輸服務的流程，然後流向信箱伺服器上的傳輸服務。

  - **安裝在不同電腦上的信箱伺服器和 Client Access Server**   在此組態中，輸入郵件流程會略過 Client Access Server。郵件會從 Edge Transport Server 上的傳輸服務流向信箱伺服器上的傳輸服務。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在周邊網路中安裝了 Exchange 2010 或 Exchange 2007 Edge Transport Server，則郵件流程一律會在 Edge Transport Server 與信箱伺服器上的傳輸服務之間直接進行。如需詳細資訊，請參閱 <a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">使用 Exchange 2010 或 2007 Edge Transport server 在 Exchange 2013</a>。</td>
</tr>
</tbody>
</table>


## 來自內部寄件者的郵件

來自組織內部的 SMTP 郵件會以下列其中一種方式透過信箱伺服器上的傳輸服務進入傳輸管線：

  - 透過接收連接器。

  - 從收取目錄或重新顯示目錄。

  - 從信箱傳輸服務。

  - 透過代理程式提交。

郵件會根據路由目的地或傳遞群組路由傳送。如需詳細資訊，請參閱[郵件路由](mail-routing-exchange-2013-help.md)。

如果郵件有外部收件者，郵件將會從信箱伺服器上的傳輸服務路由傳送至網際網路；但若將傳送連接器設定成透過 Client Access Server 代理輸出連線，則會先從信箱伺服器路由傳送至 Client Access Server 上的前端傳輸服務，然後再傳送至網際網路。如需詳細資訊，請參閱[建立電子郵件傳送至網際網路的傳送連接器](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)。

如果您在周邊網路中安裝了 Edge Transport Server，則有外部收件者的郵件一律不會透過 Client Access Server 上的前端傳輸服務來路由傳送。郵件會從信箱伺服器上的傳輸服務路由傳送至 Edge Transport Server 上的傳輸服務。

## 在 Mailbox Server 上的運輸服務

在 Exchange 2013 組織中傳送或接收的每封郵件，必須先在 信箱伺服器的傳輸服務上分類，才能路由和傳遞該郵件。郵件被分類後，將置於傳遞佇列以傳遞至目的地信箱資料庫、目的地資料庫可用性群組 (DAG)、Active Directory 站台或 Active Directory 樹系，或組織外部的目的地網域。

信箱伺服器上的傳輸服務以下列元件及流程組成：

  - **SMTP 接收**   當郵件透過傳輸服務接收時，會執行郵件內容檢查、套用傳輸規則，且會執行反垃圾郵件及反惡意程式碼 (若啟用)。SMTP 工作階段擁有一系列的事件，這些事件會先依特定的順序合作驗證郵件的內容，之後才會接受該郵件。當郵件完全通過 SMTP 接收，而且未被接收事件或反垃圾郵件和反惡意程式碼拒絕後，該郵件便會放在提交佇列中。

  - **提交**   提交是在提交佇列中放置郵件的處理程序。分類程式會一次收取一封郵件並加以分類。提交以三種方式進行：
    
      - 從「SMTP 接收」經由接收連接器。
    
      - 透過收取目錄或重新顯示目錄。這些目錄存在於信箱伺服器和 Edge Transport Server 上。複製到收取目錄或重新顯示目錄、且擁有正確格式的郵件檔案，會直接放到提交佇列中。
    
      - 透過傳輸代理程式。

  - **分類程式**   分類程式一次會從提交佇列收取一封郵件。分類程式可完成以下步驟：
    
      - 收件者解析，包含頂層定址、擴充和複本發送。
    
      - 路由解析。
    
      - 內容轉換。
    
    此外，會套用組織所定義的郵件流程規則。郵件被分類後，會根據郵件目的地被置於傳遞佇列。郵件是根據目的地郵件資料庫、DAG、Active Directory站台、Active Directory 樹系或外部網域進行佇列。

  - **SMTP 傳送**   郵件從傳輸服務路由的方式將取決於郵件收件者進行分類的相關信箱伺服器位置。郵件可路由傳送至下列其中一個位置：
    
      - 傳送至相同信箱伺服器上的信箱傳輸服務。
    
      - 傳送至屬於相同 DAG 之不同信箱伺服器上的信箱傳輸服務。
    
      - 傳送至不同 DAG、Active Directory 站台或 Active Directory 樹系中的信箱伺服器上的傳輸服務。
    
      - 透過相同信箱伺服器上的傳送連接器、不同信箱伺服器上的傳輸服務、Client Access Server 上的前端傳輸服務、或周邊網路中某部 Edge Transport Server 上的傳輸服務傳送至網際網路，以進行傳遞。

## Edge Transport Server 上的傳輸服務

Edge Transport Server 上的傳輸服務元件等同於信箱伺服器上的傳輸服務元件。但在 Edge Transport Server 上的每個處理階段中實際執行的作業並不相同。下列清單會詳細說明其中的差異。

  - **SMTP 接收**   當 Edge Transport Server 訂閱至內部 Active Directory 站台時，預設的接收連接器將自動設定成接受來自內部信箱伺服器和網際網路的郵件。當網際網路郵件送達 Edge Transport Server 時，反垃圾郵件代理程式會篩選連線和郵件內容，並在組織接受郵件時協助識別該郵件的寄件者和收件者。依預設會安裝並啟用反垃圾郵件代理程式。此外也有附件篩選和連線篩選功能可供使用，但沒有內建的惡意程式碼篩選功能。此外，傳輸規則會由編輯規則代理程式所控制。相較於信箱伺服器上的傳輸規則代理程式，Edge Transport Server 上只有些許傳輸規則條件可使用。但有些與 SMTP 連線相關的特有傳輸規則動作，是只能在 Edge Transport Server 上使用的。

  - **提交**   在 Edge Transport Server 上，郵件通常會透過接收連接器進入提交佇列。但是，收取目錄和重新顯示目錄也可供使用。

  - **分類程式**   在 Edge Transport server 上，分類是一個簡短的處理程序，可將郵件直接放入傳遞佇列中，以傳遞給內部或外部收件者。

  - **SMTP 傳送**   在 Edge Transport Server 訂閱至內部 Active Directory 站台時，將會自動建立並設定兩個傳送連接器。一個負責將輸出郵件傳送給網際網路收件者；另一個負責將來自網際網路的輸入郵件傳送給內部收件者。輸入郵件會傳送至已訂閱的 Active Directory 站台之可用信箱伺服器上的傳輸服務。

## 郵件流程文件

下列表格包含可協助您了解並管理 Exchange 2013 郵件流程的主題連結。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主題</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-routing-exchange-2013-help.md">郵件路由</a></p></td>
<td><p>郵件路由說明郵件如何在信箱伺服器間傳輸。</p></td>
</tr>
<tr class="even">
<td><p><a href="connectors-exchange-2013-help.md">連接器</a></p></td>
<td><p>連接器會定義郵件傳送到 Exchange 伺服器或從 Exchange 伺服器傳送的位置與方式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="domains-exchange-2013-help.md">網域</a></p></td>
<td><p>公認的網域會定義用於 Exchange 組織的 SMTP 位址空間。遠端網域會設定郵件格式化及傳送至外部網域的編碼設定。</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-agents-exchange-2013-help.md">傳輸代理程式</a></p></td>
<td><p>傳輸代理程式遊歷 Exchange 傳輸管線時會在郵件上作用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-high-availability-exchange-2013-help.md">傳輸高可用性</a></p></td>
<td><p>傳輸高可用性說明 Exchange 2013 如何在傳輸與傳送後的期間保留郵件的重複複本。</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-logs-exchange-2013-help.md">傳輸記錄檔</a></p></td>
<td><p>傳輸記錄會記錄郵件通過傳輸管線時的狀況。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-message-approval-exchange-2013-help.md">管理郵件核准</a></p></td>
<td><p>仲裁的傳輸需要傳送給特定收件者的核准。</p></td>
</tr>
<tr class="even">
<td><p><a href="content-conversion-exchange-2013-help.md">內容轉換</a></p></td>
<td><p>內容對話會控制外部收件者的 Transport Neutral encoding format (TNEF) 郵件對話選項，以及外部收件者的 MAPI 對話選項。</p></td>
</tr>
<tr class="odd">
<td><p><a href="dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md">Dsn 和 Ndr in Exchange 2013</a></p></td>
<td><p>傳遞狀態通知 (DSN) 為可傳送給郵件寄件者的系統郵件，例如未傳遞回報 (NDR)。</p></td>
</tr>
<tr class="even">
<td><p><a href="track-messages-with-delivery-reports-exchange-2013-help.md">使用傳遞回報追蹤郵件</a></p></td>
<td><p>[傳遞回報] 是一個郵件追蹤工具，您可以用來搜尋以特定主旨寄給或寄自組織通訊錄中之使用者的電子郵件傳遞狀態。您可追蹤組織中任何特定信箱的寄件或收件傳遞資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="message-size-limits-exchange-2013-help.md">郵件大小限制</a></p></td>
<td><p>本主題說明對郵件施加的大小及個別元件限制。</p></td>
</tr>
<tr class="even">
<td><p><a href="queue-viewer-exchange-2013-help.md">佇列檢視器</a></p></td>
<td><p>可使用 Exchange 工具箱中的佇列檢視器來檢視，並對佇列與等待佇列的郵件進行動作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="pickup-directory-and-replay-directory-exchange-2013-help.md">收取目錄和重新顯示] 目錄</a></p></td>
<td><p>收取和重新顯示目錄用於將郵件檔案插入到傳輸管線中。</p></td>
</tr>
<tr class="even">
<td><p><a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">使用 Exchange 2010 或 2007 Edge Transport server 在 Exchange 2013</a></p></td>
<td><p>本主題說明在 Exchange 2013 中使用舊版 Exchange 的 Edge 傳輸伺服器之考量事項。</p></td>
</tr>
</tbody>
</table>

