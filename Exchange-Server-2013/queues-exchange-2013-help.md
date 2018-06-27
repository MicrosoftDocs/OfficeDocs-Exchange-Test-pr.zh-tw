---
title: '佇列: Exchange 2013 Help'
TOCTitle: 佇列
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 51409252
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 佇列

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

「佇列」是訊息等候進入下一個處理階段或傳遞至目的地時的暫存位置。每個佇列都代表 Exchange Server 會以特定順序處理的一組邏輯訊息。在 Microsoft Exchange Server 2013 中，佇列中會存放進行傳遞之前、期間或之後的訊息。佇列存在於 Mailbox Server 和 Edge Transport Server 上。在本主題中，Mailbox Server 和 Edge Transport Server 皆稱為「傳輸伺服器」。

如前版的 Exchange 一樣，Exchange 2013 使用單一可延伸儲存引擎 (ESE) 資料庫來進行佇列儲存。

您可以使用 Exchange 管理命令介面以及 Exchange 工具箱中的佇列檢視器，來管理佇列和佇列中的訊息。您可以使用這些介面來檢視佇列的狀態與內容，以及詳細的訊息屬性。您也可以使用這些介面執行修改佇列或佇列中之訊息的動作。

**目錄**

  - Types of queues

  - Queue database files

  - Queue properties
    
      - NextHopSolutionKey
    
      - IncomingRate, OutgoingRate, and Velocity
    
      - Queue status
    
      - Other queue properties

  - Message properties
    
      - Message status
    
      - Other message properties

  - Manage queues and messages in queues

## 佇列類型

Exchange 2013 中使用下列佇列類型：

  - **持續性佇列**   「持續性佇列」是每個 Exchange 組織中每個傳輸伺服器上皆存在的佇列。如前版的 Exchange 一樣，Exchange 2013 中有三個持續性佇列：
    
      - **提交佇列**   「提交佇列」由分類程式使用，用來收集所有必須由傳輸伺服器上的傳輸代理程式所解析、路由傳送及處理的訊息。傳輸伺服器收到的所有訊息會進入提交佇列中進行處理。在 Mailbox Server 上，郵件會透過「接收」連接器、「收取」或「重新顯示」目錄或是「信箱傳輸提交服務」提交。在 Edge Transport Server 上，郵件通常會透過「接收」連接器提交，但也可以透過「收取」和「重新顯示」目錄。
        
        分類程式會從此佇列擷取訊息，除此之外，還會判定收件者的位置與到達該位置的路由。分類之後，訊息會移至傳遞佇列或無法存取之佇列。每個傳輸伺服器都只有一個提交佇列。在提交佇列中的訊息不能同時存在於其他佇列中。如需分類程式和傳輸管線的詳細資訊，請參閱[郵件流程](mail-flow-exchange-2013-help.md)。
    
      - **無法存取之佇列**   「無法存取之佇列」包含無法路由傳送到目的地的郵件。一般來說，無法達到的目的地是修改傳遞之路由路徑的組態變更所造成。無論目的地為何，具有無法達到的收件者的所有訊息都位於此佇列中。每個傳輸伺服器都只有一個「無法存取之佇列」。
        
        偵測到路由變更時，系統會自動重新提交「無法存取之佇列」中的訊息。因此，當導致訊息進入「無法存取的佇列」的狀況或組態錯誤獲得修復後，您就不需要採取其他動作來將訊息移出「無法存取之佇列」進行傳遞。
        
        「無法存取之佇列」通常是空的。「無法存取之佇列」如果未包含任何訊息，就不會顯示在佇列檢視器或 **Get-Queue** 結果中。
    
      - **毒藥訊息佇列**   毒藥訊息佇列是一種特殊的佇列，用來隔離在傳輸伺服器或服務故障後，被判斷為對 Exchange 2013 系統有害的訊息。郵件的內容和格式本身可能真的有害。或者，也有可能這些郵件在撰寫時是使用設計不良的代理程式，而造成 Exchange 伺服器在處理可能有問題的郵件時失敗。
        
        毒藥訊息佇列通常是空的。毒藥訊息佇列如果未包含任何訊息，就不會顯示在佇列檢視器或 **Get-Queue** 結果中。毒藥訊息佇列中的郵件絕對不會自動恢復或到期。在系統管理員手動恢復或移除郵件之前，這些郵件會保留在有害訊息佇列中。

  - **傳遞佇列**   傳遞佇列中會存放要使用 SMTP 傳遞至任何本機或遠端目的地的訊息。Exchange 伺服器間的所有訊息都是使用 SMTP 來傳輸。如果目的地是由傳遞代理程式連接器所服務，則非 SMTP 目的地也會使用傳遞佇列。. 每個傳遞佇列都包含要路由傳送至相同目的地的訊息。在實務上，一台傳輸伺服器上有多個傳遞佇列存在是無可避免的。傳遞佇列會在需要時動態建立，並且會在佇列已空以及過了到期時間時自動刪除。佇列到期時間是由 **Set-TransportService** 指令程式上的 *QueueMaxIdleTime* 參數所控制。預設值為 3 分鐘。

  - **陰影佇列**   傳輸訊息時，陰影佇列會保留訊息的備援副本。如需詳細資訊，請參閱 [陰影備援](shadow-redundancy-exchange-2013-help.md)。

  - **Safety Net**   Safety Net 會保留已經由傳輸伺服器順利傳遞之訊息的副本。Safety Net 不過是佇列資料庫中的另一個佇列，只是無法由佇列管理工具存取。如需詳細資訊，請參閱 [安全網](safety-net-exchange-2013-help.md)。

回到頁首

## 佇列資料庫檔案

所有不同的佇列都是儲存在單一 ESE 資料庫中。依預設，這個佇列資料庫位於傳輸伺服器上的 `%ExchangeInstallPath%TransportRoles\data\Queue`。

與任何 ESE 資料庫相同，佇列資料庫是使用記錄檔來接受、追蹤及維護資料。為了增強效能，所有郵件交易都會先寫入至記錄檔及記憶體，然後再寫入至資料庫檔案。檢查點檔案會追蹤資料庫已認可的交易記錄項目。在 Microsoft Exchange 傳輸服務的一般關閉期間，於交易記錄中找到的未認可資料庫變更一律會向資料庫進行認可。

循環記錄是用於佇列資料庫。這表示，交易記錄中出現過之已認可交易的歷程記錄將不會永遠留存。任何比目前檢查點還要舊的交易記錄，都會立即自動予以刪除。因此，從備份來復原佇列資料庫時，就無法重播交易記錄。

Exchange 2013 會使用「一般表格」來儲存及清除佇列資料庫中的訊息。佇列資料庫並不會在一張大型表格中處理及刪除個別訊息記錄，而是將訊息存放在多個時間型表格中，並且只有在表格中的所有訊息都已順利處理之後，才會刪除整個表格。例如，所有從下午 1:00 到下午 2:00 排入佇列的訊息，不論佇列或目的地為何，都會存放在 `1p-2p_msgs` 表格中。在下午 2:00 時，新訊息會存放在 `2p-3p_msgs` 表格中。在下午 4:00 時，會建立名為 `4p-5p_msgs` 的新表格，且只有在表格中的所有訊息都已順利處理，才會刪除整個 `1p-2p_msgs` 表格。這種刪除整個訊息表格而不是刪除個別訊息的方法，有助提升佇列資料庫所在磁碟的 I/O 效能。

下表列出構成佇列資料庫的檔案。

### 構成佇列資料庫的檔案

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>檔案</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.que</p></td>
<td><p>此佇列資料庫檔案會儲存所有佇列的郵件。</p></td>
</tr>
<tr class="even">
<td><p>Tmp.edb</p></td>
<td><p>此暫存資料庫檔案是用來驗證啟動時的佇列資料庫架構。</p></td>
</tr>
<tr class="odd">
<td><p>Trn*.log</p></td>
<td><p>此交易記錄會記錄所有的佇列資料庫變更。資料庫變更會先寫入至交易記錄，然後再認可至資料庫。Trn.log 是目前使用中的交易記錄檔。Trntmp.log 是事先建立的下一個佈建的交易記錄檔。如果現有的 Trn.log 交易記錄檔達到大小上限，則會將 Trn.log 重新命名為 Trn<em>nnnn</em>.log，其中 <em>nnnn</em> 是序號。然後，Trntmp.log 會重新命名為 Trn.log，並變成目前使用中的交易記錄檔。</p></td>
</tr>
<tr class="even">
<td><p>Trn.chk</p></td>
<td><p>此檢查點檔案會追蹤資料庫已認可的交易記錄項目。此檔案與 mail.que 檔案一律會位在相同位置。</p></td>
</tr>
<tr class="odd">
<td><p>Trnres00001.jrs</p>
<p>Trnres00002.jrs</p></td>
<td><p>這些保留交易記錄檔是作為預留位置。只有在含有交易記錄的硬碟機空間用完而完全停止佇列資料庫時，才會使用它們。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 設定佇列資料庫的選項

您可以透過在 `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML 應用程式組態檔中新增或修改索引鍵，來設定佇列資料庫。此檔案與 Microsoft Exchange Transport 服務相關聯。您對 EdgeTransport.exe.config 檔所做的變更，在重新啟動 Microsoft Exchange Transport 服務後才會生效。

EdgeTransport.exe.config 檔的 `<appSettings>` 區段，是您可以新增索引鍵或修改現有索引鍵的位置。如果特定索引鍵不存在，可以手動新增它來變更其值。

下表說明 EdgeTransport.exe.config 檔中可用的佇列資料庫索引鍵。

### EdgeTransport.exe.config 檔中可用的訊息佇列資料庫索引鍵

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>按鍵</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabaseBatchSize</em></p></td>
<td><p>40</p></td>
<td><p>此索引鍵可指定在執行之前，可先組成群組的資料庫 I/O 作業數目。依預設，此索引鍵不存在於 EdgeTransport.exe.config 檔中。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseBatchTimeout</em></p></td>
<td><p>100</p></td>
<td><p>此索引鍵可指定資料庫在執行多個資料庫 I/O 作業之前，等待這些資料庫 I/O 作業組成群組的時間上限 (毫秒)。如果符合下列條件，則會執行資料庫 I/O 作業，而不再繼續等待：</p>
<ul>
<li><p>尚未達到 <em>QueueDatabaseBatchSize</em> 索引鍵所指定的資料庫 I/O 作業數目。</p></li>
<li><p>已超過 <em>QueueDatabaseBatchTimeout</em> 索引鍵所指定的時間。</p></li>
</ul>
<p>依預設，此索引鍵不存在於 EdgeTransport.exe.config 檔中。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxConnections</em></p></td>
<td><p>4</p></td>
<td><p>此索引鍵可指定可以開啟的 ESE 資料庫連線數目。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingBufferSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>此索引鍵可指定將交易記錄寫入至交易記錄檔之前，用來快取交易記錄的記憶體。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseLoggingFileSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>此索引鍵可指定交易記錄檔的大小上限。達到記錄檔大小上限時，會開啟新的記錄檔。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>此索引鍵可指定佇列資料庫記錄檔的預設目錄。如需關於如何變更佇列資料庫位置的指示，請參閱<a href="change-the-location-of-the-queue-database-exchange-2013-help.md">變更佇列資料庫的位置</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxBackgroundCleanupTasks</em></p></td>
<td><p>32</p></td>
<td><p>此索引鍵可指定任何時候可以佇列至資料庫引擎執行緒集區的背景清理工作項目數目上限。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragEnabled</em></p></td>
<td><p>True</p></td>
<td><p>此索引鍵可啟用或停用排定的郵件佇列資料庫線上磁碟重組。依預設，此索引鍵不存在於 EdgeTransport.exe.config 檔中。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseOnlineDefragSchedule</em></p></td>
<td><p><code>1:00:00</code> 或上午 1:00。</p></td>
<td><p>此索引鍵可指定一天中要啟動郵件佇列資料庫線上磁碟重組的時間 (24 小時制)。若要指定值，請輸入值作為時間：<em>hh:mm:ss</em>，其中 <em>h</em> = 小時數、<em>m</em> = 分鐘數，而 <em>s</em> = 秒數。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragTimeToRun</em></p></td>
<td><p><code>3:00:00</code> 或 3 小時</p></td>
<td><p>此索引鍵可指定允許線上磁碟重組工作執行的時間長度。即使磁碟重組工作未在指定的時間內完成，佇列資料庫仍然會保留一致狀態。若要指定值，請輸入時間範圍格式：<em>hh:mm:ss</em>，其中 <em>h</em> = 小時數、<em>m</em> = 分鐘數，而 <em>s</em> = 秒數。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>此索引鍵可指定佇列資料庫檔案的預設目錄。如需關於如何變更佇列資料庫位置的指示，請參閱<a href="change-the-location-of-the-queue-database-exchange-2013-help.md">變更佇列資料庫的位置</a>。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您安裝 Exchange 累計更新 (CU) 後，將會覆寫您在 Exchange XML 應用程式組態檔 (例如 Client Access Server 上的 web.config 檔案，或 Mailbox Server 上的 EdgeTransport.exe.config 檔案) 中任何自訂的個別伺服器設定。請務必儲存此資訊，以便安裝後能輕易地重新設定伺服器。在安裝 Exchange CU 後，您必須重新配置這些設定。</td>
</tr>
</tbody>
</table>


回到頁首

## 佇列屬性

一個佇列有許多內容用來描述該佇列之目的與狀態。有些佇列內容會在佇列建立時套用，然後就不變更。有些內容則包含狀態、大小、時間或其他經常更新的指標。

回到頁首

## NextHopSolutionKey

Microsoft Exchange Transport 服務中之分類程式的路由元件會為訊息選取目的地，而此目的地會用來建立傳遞佇列。系統會將目的地戳記到每個收件者上，作為 **NextHopSolutionKey** 屬性。**NextHopSolutionKey** 屬性的每個唯一值相當於一個個別的傳遞佇列。

**NextHopSolutionKey** 屬性包含以下欄位：

  - **DeliveryType**   此欄位的值代表訊息分類的結果，以及傳輸服務預定如何將訊息傳輸至下一個躍點，該躍點可能是訊息的最終目的地，也可能是途中的中繼躍點。傳輸服務會根據目標路由目的地或傳遞群組，對 **DeliveryType** 使用預先定義的值清單。

  - **NextHopDomain**   此欄位會根據 **DeliveryType** 欄位的值來使用特定的值。對於傳遞佇列，此欄位的值實際上就是佇列的名稱。**NextHopDomain** 的值不一定是網域名稱。例如，這個值可以是目標 Active Directory 站台或資料庫可用性群組 (DAG) 的名稱。請將此欄位視為下一個躍點名稱，其中的值是路由目的地或目標傳遞群組的名稱。

  - **NextHopConnector**   此欄位會根據 **DeliveryType** 欄位的值來使用特定的值。這個值一律以 GUID 表示。如果未使用此欄位，則值為全部是零的 GUID。**NextHopConnector** 的值不一定是連接器的 GUID。例如，這個值可以是目標 Active Directory 站台或 DAG 的 GUID。請將此欄位視為下一個躍點 GUID，其中的值是路由目的地或目標傳遞群組的 GUID。

Exchange 2013 也會根據 **DeliveryType** 的值，將 **NextHopCategory** 內容新增到佇列中。**NextHopCategory** 的值為 `External` 或 `Internal`。值為 `External` 表示佇列的下一個躍點位於 Exchange 組織外部。值為 `Internal` 表示佇列的下一個躍點位於 Exchange 組織內部。請注意，要傳送給外部收件者的訊息，可能需要先經過一或多個內部躍點才會傳遞至外部。

下表說明 **DeliveryType**、**NextHopCategory**、**NextHopDomain** 及 **NextHopConnector** 的值。


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>佇列檢視器中的傳遞類型</th>
<th>命令介面中的 DeliveryType</th>
<th>描述</th>
<th>NextHopCategory</th>
<th>NextHopDomain</th>
<th>NextHopConnector</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>傳遞代理程式</strong></p></td>
<td><p><strong>DeliveryAgent</strong></p></td>
<td><p>佇列中會存放要傳遞給非 SMTP 位址空間中之收件者的訊息。訊息會使用本機伺服器上所設定的傳遞代理程式連接器來傳遞。</p></td>
<td><p>External</p></td>
<td><p>這個值是傳遞代理程式連接器上設定之目的地位址空間。</p></td>
<td><p>這個值是傳遞代理程式連接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p>佇列中會存放要傳遞給 SMTP 位址空間中之收件者的訊息。訊息會使用本機伺服器上所設定的傳送連接器來傳遞。傳送連接器已設定成使用 DNS 路由。</p></td>
<td><p>External</p></td>
<td><p>這個值是傳送連接器上設定之目的地位址空間。例如，<code>contoso.com</code>。</p></td>
<td><p>這個值是傳送連接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p>佇列中會存放要傳遞給非 SMTP 位址空間中之收件者的訊息。訊息會使用本機伺服器上所設定的外部連接器來傳遞。</p></td>
<td><p>External</p></td>
<td><p>這個值是外部連接器上設定之目的地位址空間。</p></td>
<td><p>這個值是外部連接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p>佇列中會存放要傳遞給 SMTP 位址空間中之收件者的訊息。訊息會使用本機伺服器上所設定的傳送連接器來傳遞。傳送連接器已設定成使用智慧主機路由。</p></td>
<td><p>External</p></td>
<td><p>這個值是傳送連接器上設定之智慧主機的清單。可以以 FQDN、IP 位址或兩者皆有的形式來設定智慧主機。值可以是下列其中一項：</p>
<ul>
<li><p><strong>FQDN</strong>   語法為 <code>&lt;FQDN1,FQDN2,...&gt;</code>。例如，<code>smarthost01.contoso.com</code> 或 <code>smarthost01.contoso.com,smarthost02.fabrikam.com</code>。</p></li>
<li><p><strong>IP 位址</strong>   語法為 <code>&lt;[IPAddress1],[IPAddress2],...&gt;</code>。例如，<code>[10.10.10.100]</code> 或 <code>[10.10.10.100],[10.10.10.101]</code>。</p></li>
<li><p><strong>FQDN 和 IP 位址</strong>   語法為 <code>&lt;[IPAddress1],FQDN1,...&gt;</code>，取決於傳送連接器上如何列出智慧主機而定。例如，<code>[172.17.17.7],relay.tailspintoys.com</code> 或 <code>mail.contoso.com,[192.168.1.50]</code>。</p></li>
</ul></td>
<td><p>這個值是傳送連接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SMTP 傳遞至信箱</strong></p></td>
<td><p><strong>SmtpDeliveryToMailbox</strong></p></td>
<td><p>佇列中會存放要傳遞給 Exchange 2013 信箱收件者的訊息。目的地信箱資料庫是在下列其中一個位置中：</p>
<ul>
<li><p>本機 Exchange 2013 Mailbox Server。</p></li>
<li><p>相同 DAG 中的 Exchange 2013 Mailbox Server。</p></li>
<li><p>非 DAG 環境內之相同 Active Directory 站台中的 Exchange 2013 Mailbox Server。</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>這個值是目的地信箱資料庫的名稱。例如，<code>Mailbox Database 0471695037</code>。</p></td>
<td><p>這個值是目標信箱資料庫的 GUID。例如，<code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>對傳送連接器來源伺服器的 SMTP 轉送</strong></p></td>
<td><p><strong>SmtpRelayToConnectorSourceServers</strong></p></td>
<td><p>佇列中會存放要傳遞給 SMTP 或非 SMTP 收件者的訊息。訊息會使用遠端傳輸伺服器上所設定之傳送連接器、傳遞代理程式連接器或外部連接器來傳遞。遠端傳輸伺服器可以是 Exchange 2013 Mailbox Server，或是來自前版 Exchang 的 Exchange 2007 或 Exchange 2010 Hub Transport Server。遠端伺服器可能位於本機 Active Directory 站台或是遠端 Active Directory 站台中。</p></td>
<td><p>Internal</p></td>
<td><p>這個值是目的地傳送連接器、傳遞代理程式連接器或外部連接器的名稱。例如，<code>Contoso.com Send Connector</code>。</p></td>
<td><p>這個值是目的地傳送連接器、傳遞代理程式連接器或外部連接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>對資料庫可用性群組的 SMTP 轉送</strong></p></td>
<td><p><strong>SmtpRelayToDag</strong></p></td>
<td><p>佇列中會存放要傳遞給 Exchange 2013 信箱收件者的訊息，其中目的地信箱資料庫位於遠端 DAG 中。遠端 DAG 可能位於本機 Active Directory 站台或是遠端 Active Directory 站台中。</p></td>
<td><p>Internal</p></td>
<td><p>這個值是目的地 DAG 的名稱。例如，<code>DAG1</code>。</p></td>
<td><p>這個值是目的地 DAG 的 GUID。例如，<code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code></p></td>
</tr>
<tr class="even">
<td><p><strong>對信箱傳遞群組的 SMTP 轉送</strong></p></td>
<td><p><strong>SmtpRelayToMailboxDeliveryGroup</strong></p></td>
<td><p>佇列中會存放要傳遞給舊版信箱收件者的訊息，其中目的地信箱位於 Exchange 2007 或 Exchange 2010 Mailbox Server 上。訊息是跟與目的地信箱執行相同 Exchange 版本的 Hub Transport Server 有關。目的地 Hub Transport Server 可能位於本機 Active Directory 站台或是遠端 Active Directory 站台中。</p></td>
<td><p>Internal</p></td>
<td><p>佇列名稱使用下列語法：<code>Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion&gt;</code>，其中 <em>&lt;ADSiteName&gt;</em> 是目的地 Active Directory 站台的名稱，而 <em>&lt;ExchangeVersion&gt;</em> 是 Mailbox Server 上的 Exchange 版本。</p></td>
<td><p>這個值是空白的。</p></td>
</tr>
<tr class="odd">
<td><p><strong>對遠端 Active Directory 站台的 SMTP 轉送</strong></p></td>
<td><p><strong>SmtpRelayToRemoteActiveDirectorySite</strong></p></td>
<td><p>佇列中會存放要傳遞至遠端目的地的訊息，而路由拓撲需要透過特定 Active Directory 站台來路由傳送訊息。這個站台是到最終目的地途中的中繼躍點。在下列情況下會發生這種狀況：</p>
<ul>
<li><p>訊息需要透過中樞站台來路由傳送。</p></li>
<li><p>訊息需要透過 Edge Transport Server (其訂閱了遠端 Active Directory 站台) 上所設定的傳送連接器來傳遞。</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>這個值是目標 Active Directory 站台名稱。例如，<code>NorthAmericanSite</code>。</p></td>
<td><p>這個值是目標 Active Directory 站台的 GUID。例如，<code>bfd6c3df-5b65-8bfb-53f1f2c0d55c</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>對指定 Exchange Server 的 SMTP 轉送</strong></p></td>
<td><p><strong>SmtpRelayToServers</strong></p></td>
<td><p>佇列中會存放要傳遞給為特定擴充伺服器所設定之通訊群組的訊息。擴充可以是 Exchange 2013 Mailbox Server，或是 Exchange 2007 或 Exchange 2010 Hub Transport Server。伺服器可能位於本機 Active Directory 站台或遠端 Active Directory 站台中。</p></td>
<td><p>Internal</p></td>
<td><p>這個值是目標擴充伺服器的 FQDN。例如，<code>mailbox01.contoso.com</code>。</p></td>
<td><p>這個值是 <code>00000000-0000-0000-0000-000000000000</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>對 Edge Transport Server 之 Active Directory 站台中的 SMTP 轉送</strong></p></td>
<td><p><strong>SmtpRelayWithinAdSiteToEdge</strong></p></td>
<td><p>佇列中會存放要傳遞至 SMTP 位址空間的訊息。訊息會透過 Edge Transport Server (其訂閱了本機 Active Directory 站台) 上所設定的傳送連接器來傳遞。</p></td>
<td><p>Internal</p></td>
<td><p>這個值是將輸出的網際網路郵件從組織傳送至網際網路時所使用的傳送連接器的名稱。這個傳送連接器會自動由 Edge 訂閱所建立，且命名為 <code>EdgeSync - &lt;ADSiteName&gt; to Internet</code>。<em>&lt;ADSiteName&gt;</em> 是 Edge Transport Server 所訂閱之本機 Active Directory 站台的名稱。</p></td>
<td><p>這個值是傳送連接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>活動訊號</strong></p></td>
<td><p><strong>活動訊號</strong></p></td>
<td><p>這個值是已保留供 Microsoft 內部使用。如需活動訊號的相關資訊，請參閱<a href="shadow-redundancy-exchange-2013-help.md">陰影備援</a>。</p></td>
<td><p>不適用</p></td>
<td><p>不適用</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p><strong>陰影備援</strong></p></td>
<td><p><strong>ShadowRedundancy</strong></p></td>
<td><p>佇列會將訊息保存在陰影佇列中。陰影佇列會在傳輸時保留備援副本，以防主要訊息無法順利傳遞。如需詳細資訊，請參閱 <a href="shadow-redundancy-exchange-2013-help.md">陰影備援</a>。</p></td>
<td><p>Internal</p></td>
<td><p>這個值是主要伺服器的 FQDN，陰影佇列即在為其保存主要訊息的備援副本。例如，<code>mailbox01.contoso.com</code>。</p></td>
<td><p>這個值是 <code>00000000-0000-0000-0000-000000000000</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>Undefined</strong></p></td>
<td><p><strong>Undefined</strong></p></td>
<td><p>只有在提交佇列或毒藥訊息佇列上才使用這個值。</p></td>
<td><p>Internal</p></td>
<td><p>若是提交佇列，這個值是 <code>Submisssion</code>。若是毒藥訊息佇列，這個值是 <code>Poison Message</code>。</p></td>
<td><p>這個值是 <code>00000000-0000-0000-0000-000000000000</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>無法存取</strong></p></td>
<td><p><strong>無法存取</strong></p></td>
<td><p>只有在「無法存取之佇列」上才使用這個值。</p></td>
<td><p>Internal</p></td>
<td><p>這個值是 <code>Unreachable Domain</code>。</p></td>
<td><p>這個值是 <code>00000000-0000-0000-0000-000000000000</code>。</p></td>
</tr>
</tbody>
</table>


請注意 Exchange 2013 支援 **DeliveryType** 的舊版值，以便與舊版 Exchange 相容。這些值可在佇列檢視器和命令介面中使用，但 Exchange 2013 不會使用它們。這些舊版 **DeliveryType** 值包括：

  - **MapiDelivery**   佇列中會存放要由 Exchange 2007 或 Exchange 2010 Hub Transport Server 傳遞至本機 Active Directory 站台中 Exchange 2007 或 Exchange 2010 Mailbox Server 上之信箱的訊息。

  - **SmtpRelayWithinAdSite**   佇列中會存放要由 Exchange 2007 或 Exchange 2010 Hub Transport Server 傳遞至相同 Active Directory 站台中另一台 Hub Transport Server 的訊息。目的地 Hub Transport Server 可以是連接器的來源伺服器，或是通訊群組擴充伺服器。

  - **SmtpRelaytoTiRg**   佇列中會存放要由 Exchange 2007 或 Exchange 2010 Hub Transport Server 傳遞至 Exchange Server 2003 路由群組的訊息。目的地伺服器可以是連接器的來源伺服器、通訊群組擴充伺服器或 Exchange 2003 Bridgehead 伺服器。

回到頁首

## IncomingRate、OutgoingRate 以及 Velocity

Exchange 2013 會測量訊息進入及離開佇列的速度，並將這些值存放在佇列內容中。您可以使用這些速率作為佇列和傳輸伺服器健康狀況的指標。這些內容如下：

  - **IncomingRate**   這項內容是訊息進入佇列的速率。
    
    這個值是每 5 秒進入佇列的訊息數，除以最後 60 秒所得的平均值來計算。其公式可以表示成 `(i1+i2+i3+i4+i5+i6)/6`，其中 i*n* = 5 秒內的內送訊息數。

  - **OutgoingRate**   這項內容是訊息離開佇列的速率。
    
    這個值是每 5 秒離開佇列的訊息數，除以最後 60 秒所得的平均值來計算。其公式可以表示成 `(o1+o2+o3+o4+o5+o6)/6`，其中 o*n* = 5 秒內的外送訊息數。

  - **Velocity**   這項內容是佇列的清空速率，並且是以 **OutgoingRate** 的值減去 **IncomingRate** 的值來計算。
    
    如果 **Velocity** 的值大於 0，則訊息離開佇列的速度比進入佇列的速度快。
    
    如果 **Velocity** 的值等於 0，則訊息離開佇列的速度和進入佇列的速度一樣快。這也是佇列未作用時，您將會看到的值。
    
    如果 **Velocity** 的值小於 0，則訊息進入佇列的速度比離開佇列的速度快。

基本上，**Velocity** 為正值表示佇列正處於有效清空的健康狀態，而 **Velocity** 為負值表示佇列並未有效清空。不過，您也需要考慮 **IncomingRate**、**OutgoingRate** 及 **MessageCount** 內容的值，以及佇列之 **Velocity** 值的強度。例如，如果佇列具有高負值的 **Velocity**、很小的 **MessageCount** 值、很小的 **OutgoingRate** 值以及很大的 **IncominRate** 值，就可以很肯定地說該佇列未正確清空。不過，如果佇列的 **Velocity** 為很接近零的負值，而且佇列的 **IncomingRate**、**OutgoingRate** 及 **MessageCount** 值也很小，則表示此佇列沒什麼問題。

回到頁首

## 佇列狀態

佇列的目前狀態是存放在佇列的 **Status** 內容中。佇列可以擁有下列其中一種狀態值：

  - **使用中**   佇列正主動傳輸訊息。

  - **正在連線**   佇列正連線至下一個躍點。

  - **準備就緒**   佇列最近曾傳輸訊息，但佇列現在是空的。

  - **重試**   上次嘗試自動或手動連線已失敗，佇列正等待重試連線。

  - **暫停**   系統管理員已手動擱置佇列以防止傳遞訊息。新的訊息可以進入佇列，而已開始傳輸至下一個躍點的訊息，則會完成傳遞並離開佇列。其他訊息則不會離開佇列，直到系統管理員手動繼續佇列為止。請注意，擱置佇列並不會使佇列中個別訊息的狀態變更。
    
    您可以暫停狀態為 Active 或 Retry 的佇列。也可以暫停 Unreachable 佇列和 Submission 佇列。
    
    如果您暫停無法存取之佇列，則系統在偵測到組態更新時，就不會自動將訊息重新提交至分類程式。若要自動重新提交這些訊息，您需要手動繼續「無法存取之佇列」。如果暫停 Submission 佇列，則在佇列重新繼續運作之前，分類程式不會收取郵件。

回到頁首

## 其他佇列內容

有些其他佇列內容只要看名稱就能明白其用途。您可以使用大部分的佇列內容作為篩選選項。藉由指定篩選準則，您可以快速地尋找佇列並對佇列採取行動。如需可篩選之佇列內容的完整說明，請參閱[佇列篩選器](queue-filters-exchange-2013-help.md)。

在這裡有個值得一提的重要佇列內容，那便是負責顯示佇列中之訊息數目的 **MessageCount** 內容。這項內容是佇列健康狀況的重要指標。例如，如果有個傳遞佇列包含大量訊息，而且訊息的數量還持續成長、未曾減少過，則表示您可能需要注意路由或傳輸管線問題。

回到頁首

## 郵件屬性

在佇列中，一個訊息有許多內容。其中許多內容均反映當初用於建立訊息的資訊。有些訊息狀態和資訊內容，嚴重受到佇列上的相對應內容所影響。不過，個別訊息的值可能會與佇列上相對應內容的值不同。有些內容則包含狀態、時間或其他經常更新的指標。

回到頁首

## 訊息狀態

訊息的目前狀態是存放在訊息的 **Status** 內容中。郵件可具有下列其中一個狀態值：

  - **Active** 郵件若位於傳遞佇列中，即會傳遞至其目的地。郵件若位於提交佇列中，則會由分類程式進行處理。

  - **Locked**   這個值已保留供 Microsoft 內部使用，不會用於內部部署 Exchange 組織中。

  - **PendingRemove**   訊息已被系統管理員刪除，但訊息已開始傳輸至下一個躍點。若傳遞因錯誤而結束，導致郵件重新進入佇列中，郵件就會被刪除。否則，會繼續傳遞。

  - **PendingSuspend**   訊息已被系統管理員暫停，但訊息已開始傳輸至下一個躍點。若傳遞因錯誤而暫停，導致郵件重新進入佇列中，郵件就會被刪除。否則，會繼續傳遞。

  - **準備就緒**   郵件已在佇列中準備就緒可進行處理。

  - **Retry**   上次自動或手動嘗試對此郵件所在佇列進行連線失敗。訊息正在等候下一次自動重試佇列連線。

  - **Suspended**   訊息已被系統管理員手動暫停。所有有害訊息佇列中的郵件處於永久擱置的狀態。

回到頁首

## 其他訊息內容

有些其他訊息內容只要看名稱就能明白其用途。您可以使用大部分的訊息內容作為篩選選項。指定篩選準則後，您就可以迅速地找出郵件並採取動作。如需可篩選之訊息內容的完整說明，請參閱[訊息篩選器](message-filters-exchange-2013-help.md)。

回到頁首

## 管理佇列與佇列中的訊息

佇列檢視器以及幾乎所有的佇列與訊息管理指令程式，都限用於單一的 Exchange Server。您可以在個別或多個佇列或訊息上進行檢視和操作，但只能在某個特定伺服器上進行。

Exchange 2013 引入的 **Get-QueueDigest** 指令程式，可提供特定範圍中所有伺服器上佇列狀態的高階和彙總檢視，例如，DAG、Active Directory 站台、伺服器清單，或是整個 Active Directory 樹系。請注意，結果中不會包含周邊網路中已訂閱的 Edge Transport Server 上的佇列。此外，**Get-QueueDigest** 也可在 Edge Transport Server 上使用，但結果只會顯示 Edge Transport Server 上的佇列。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>依預設，<strong>Get-QueueDigest</strong> 指令程式會顯示包含十封郵件以上的傳遞佇列，而且會是一到二分鐘之前的結果。如需如何變更這些預設值的指示，請參閱<a href="configure-get-queuedigest-exchange-2013-help.md">設定 Get-QueueDigest</a>。</td>
</tr>
</tbody>
</table>


下表說明您可以在佇列或是佇列中的訊息上執行的管理工作。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>工作</th>
<th>描述</th>
<th>要使用的工具</th>
<th>指示</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>檢視及篩選伺服器上的佇列</p></td>
<td><p>此動作會顯示傳輸伺服器上的一或多個佇列。您可以使用結果來對佇列採取動作。</p></td>
<td><p>佇列檢視器或 <strong>Get-Queue</strong> 指令程式。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理佇列</a></p></td>
</tr>
<tr class="even">
<td><p>檢視及篩選在特定 DAG、特定 Active Directory 站台或整個 Active Directory 樹系中之特定伺服器上的佇列。</p></td>
<td><p>此動作會顯示在已定義的範圍 (伺服器、DAG、Active Directory 站台或是整個 Active Directory 樹系) 中佇列的彙總檢視。</p></td>
<td><p>只有 <strong>Get-QueueDigest</strong> 指令程式</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理佇列</a></p></td>
</tr>
<tr class="odd">
<td><p>擱置佇列</p></td>
<td><p>此動作可暫時防止傳遞目前在佇列中的訊息。佇列會繼續接受新訊息，但是訊息不會離開佇列。</p></td>
<td><p>佇列檢視器或 <strong>Suspend-Queue</strong> 指令程式。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理佇列</a></p></td>
</tr>
<tr class="even">
<td><p>繼續佇列</p></td>
<td><p>此動作的效果跟擱置佇列的動作相反，可讓佇列的訊息繼續傳遞。</p></td>
<td><p>佇列檢視器或 <strong>Resume-Queue</strong> 指令程式。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理佇列</a></p></td>
</tr>
<tr class="odd">
<td><p>重試佇列</p></td>
<td><p>此動作會立即嘗試連線至下一個躍點。在無手動干預的情況下，當連線至下一個躍點失敗時，就會一直嘗試連線，每次嘗試之間相隔特定的時間間隔，以特定次數為限。</p>
<p>不論是手動或自動嘗試連線，只要一嘗試連線，就會使下次重試時間重設。如需詳細資訊，請參閱 <a href="message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md">郵件重試、 重新提交、 及到期時間間隔</a>。</p></td>
<td><p>佇列檢視器或 <strong>Retry-Queue</strong> 指令程式。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理佇列</a></p></td>
</tr>
<tr class="even">
<td><p>重新提交佇列中的郵件</p></td>
<td><p>此動作會讓佇列中的訊息重新提交至提交佇列，並透過分類程序返回。</p></td>
<td><p><strong>Retry-Queue</strong> 搭配 <em>Resubmit</em> 參數</p>
<p>請注意，您可以使用佇列檢視器來重新提交訊息，但只能從毒藥訊息佇列來進行。若要重新提交毒藥訊息佇列中的訊息，您可以在佇列檢視器中恢復訊息，或是使用 <strong>Resume-Message</strong> 指令程式。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理佇列</a></p></td>
</tr>
<tr class="odd">
<td><p>擱置佇列中的訊息</p></td>
<td><p>此動作會暫時防止傳遞訊息。您可以使用暫停訊息動作來防止訊息傳遞到特定佇列中的所有收件者，或是所有佇列中的所有收件者。</p></td>
<td><p>佇列檢視器或 <strong>Suspend-Message</strong> 指令程式。</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">管理佇列中的郵件</a></p></td>
</tr>
<tr class="even">
<td><p>恢復佇列中的訊息</p></td>
<td><p>此動作的效果跟暫停訊息的動作相反，可讓佇列的訊息繼續傳遞。您可以使用繼續訊息動作來繼續將訊息傳遞到特定佇列中的所有收件者，或是所有佇列中的所有收件者。</p></td>
<td><p>佇列檢視器或 <strong>Resume-Message</strong> 指令程式。</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">管理佇列中的郵件</a></p></td>
</tr>
<tr class="odd">
<td><p>從佇列移除訊息</p></td>
<td><p>此動作會永久防止傳遞訊息。您可以使用移除訊息動作來防止訊息傳遞到指定佇列中的任何收件者，或是所有佇列中的所有收件者。您也可以設定移除訊息動作，讓它在移除訊息時傳送未傳遞回報 (NDR) 給寄件者。</p></td>
<td><p>佇列檢視器或 <strong>Remove-Message</strong> 指令程式。</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">管理佇列中的郵件</a></p></td>
</tr>
<tr class="even">
<td><p>從佇列匯出訊息</p></td>
<td><p>此動作會將訊息複製到您指定的檔案路徑。此動作並不會將訊息從佇列中刪除，但是會將訊息副本儲存到檔案位置。如此可便於系統管理員或組織中的管理人員日後檢查訊息。在匯出訊息前，您必須擱置佇列中的訊息，使得進行一般的傳遞作業不會在匯出程序期間繼續。</p></td>
<td><p>只有 <strong>Export-Message</strong> 指令程式。</p></td>
<td><p><a href="export-messages-from-queues-exchange-2013-help.md">從佇列匯出訊息</a></p></td>
</tr>
</tbody>
</table>


回到頁首

