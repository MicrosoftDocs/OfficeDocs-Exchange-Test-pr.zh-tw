---
title: '了解 Exchange 2013 分頁清空: Exchange 2013 Help'
TOCTitle: 了解 Exchange 2013 分頁清空
ms:assetid: 0ca7b188-efbc-4c0d-bcfe-5138cffc803c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg549096(v=EXCHG.150)
ms:contentKeyID: 61620005
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解 Exchange 2013 分頁清空

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

## Exchange 2013 的分頁清空

*「清空」*是一種安全性機制，以零或二進位模式來覆寫已刪除的資料，使已刪除的資料更加難以復原。在 Exchange Server 2013 中，ESE 資料庫使用*「頁面」*作為儲存單位來實作*「分頁清空」*。依預設會啟用分頁清空，且無法停用。分頁清空作業會記錄在交易記錄檔中，以便使用類似方式對所有資料庫副本進行分頁清空。在主動資料庫上將頁面清空會在被動資料庫複本上清空此頁面。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可延伸儲存引擎 (ESE) 沒有任何機制，可用來將重複利用已清空分頁的優先順序排在配置新空間之前。已指派循序空間配置的資料表會刻意略過分散或清空的分頁，優先使用新的或可用的循序頁面。此方法可減少資料庫 IOP。</td>
</tr>
</tbody>
</table>


在 Exchange 2013 中，分頁清空可降低伺服器在執行清空功能時造成的效能影響。這包括：

  - **最佳化的儲存和網路容量**   ESE 會將分頁清空記錄寫入交易記錄檔，而不是記錄整個分頁映像。此方法可減少記錄寫入 I/O，並降低傳送記錄檔時的頻寬需求。

  - **最佳化資料庫磁碟 I/O**  在 \[ Exchange 2010 RTM 舊版分頁清空發生只能在備份期間或在排定的維護期間和其造成重大的資料庫磁碟 I/O。在Exchange 2010 SP1 和更新版本 （包括Exchange 2013)、 頁面清空發生根據預設，交易次發生的情況。在大多數的情況下，清空硬刪除後立即發生。此設計可讓運用引擎，可確保該 dirty 頁面保持資料庫快取中的時間量使其他頁面更新後發生在關閉鄰近不會造成其他的資料庫寫入 I/o 時間的檢查點深度功能的資料庫。因為此設計、 分頁清空有任何重大的資料庫 I/O 影響，這是預設啟用的原因。

## 在 ESE 資料庫中實作分頁清空

分頁清空會以二進位模式覆寫實刪除的記錄。分頁清空模式是 ESE 引擎作業所特有，且對執行階段作業與維護作業而言是不同的。下表列出對應至特定執行階段作業的填滿圖樣。

### ESE 執行階段期間的分頁清空填入模式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ESE 執行階段作業</th>
<th>填滿圖樣</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>取代</p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p>記錄/長數值刪除</p></td>
<td><p>D</p></td>
</tr>
<tr class="odd">
<td><p>釋放的頁面空間</p></td>
<td><p>H</p></td>
</tr>
</tbody>
</table>


下表列出對應至特定作業的填滿圖樣，這些作業是在 ESE 背景資料庫維護期間進行。

### ESE 背景資料庫維護期間的分頁清空填入模式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ESE 背景資料庫維護作業</th>
<th>填滿圖樣</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>記錄刪除</p></td>
<td><p>D</p></td>
</tr>
<tr class="even">
<td><p>長數值刪除</p></td>
<td><p>L</p></td>
</tr>
<tr class="odd">
<td><p>部分使用頁面的已釋放頁面空間</p></td>
<td><p>Z</p></td>
</tr>
<tr class="even">
<td><p>未使用頁面的已釋放頁面空間</p></td>
<td><p>U</p></td>
</tr>
</tbody>
</table>


## 背景資料庫維護

背景資料庫維護是一個持續對資料庫進行總和檢查和掃描的程序。主要功能是進行資料庫頁面的總和檢查，但也會負責清除空間及清空由於儲存區損毀而未清空的記錄和頁面。背景資料庫維護處理速度約為每一資料庫每秒 1 MB。如果及時分頁清空為第一優先，您可以減少資料庫大小，以確保在損毀復原情況下，分頁清空能在較短的期間 (例如，24 小時) 內進行。

背景資料庫維護是連續的處理程序，因此沒有任何與其開始和完成關聯的事件。您可以讀取效能計數器的值，以追蹤背景資料庫維護的進度：

  - MSExchange Database -\> Instances -\> Database Maintenance Duration

此計數器會指出自從給定資料庫上次完成維護以來經過的秒數。

## ESE 資料庫分頁清空的處理程序

下表討論資料庫刪除案例，以及分頁清空功能發生的時間。

### ESE 背景資料庫維護

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>資料庫刪除案例</th>
<th>清空資料庫資料 的 ESE 處理程序和時段</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>案例 1：單一項目復原已停用，且使用者從 [可復原的項目] 資料夾清除項目。</p></li>
<li><p>案例 2：單一項目復原已停用，且 [可復原的項目] 保留期間設為零。</p></li>
<li><p>案例 3：單一項目復原已啟用，且項目是否過期取決於刪除項目保留期間。</p></li>
</ul></td>
<td><p>非同步執行緒會以二進位模式覆寫刪除的資料。此動作會在記錄刪除的幾毫秒內發生。如果儲存區處理程序在非同步清空工作仍未完成時損毀 (或者由於版本儲存區成長而取消版本儲存區清理)，則會在背景資料庫維護處理該區段的資料庫時完成清空。</p></td>
</tr>
<tr class="even">
<td><p>檢視案例：Outlook/Outlook Web 資料夾檢視 (例如，[交談] 檢視) 中項目的到期</p></td>
<td><p>資料清空會在背景資料庫維護處理該區段的資料庫時進行。</p></td>
</tr>
<tr class="odd">
<td><p>移動信箱/刪除信箱案例：刪除來源信箱 (暫放中刪除的信箱到期)</p></td>
<td><p>資料清空會在背景資料庫維護處理該區段的資料庫時進行。</p></td>
</tr>
</tbody>
</table>


## 監控分頁清空行為

您可以檢視兩個 ESE 計數器來測量和監督分頁清空功能：

  - MSExchange 資料庫-\>清空的資料庫維護頁面：指出自上次叫用效能計數器以來，由資料庫引擎清空的頁數。

  - MSExchange 資料庫-\>清空的資料庫維護頁面‎/秒：指出分頁清空的速率。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要了解如何啟用這些計數器，請參閱 ＜<a href="https://go.microsoft.com/fwlink/p/?linkid=101194">如何啟用延伸的 ESE 效能計數器</a>。</td>
</tr>
</tbody>
</table>


分頁清空是一項資料庫維護功能，因此執行階段交易之分頁清空，以及由於背景資料庫維護而進行之分頁清空的相關效能資訊，都會包含在這些計數器中。

## 不清空分頁的信箱資料類型

下列信箱資料類型未佈建分頁清空：

  - 信箱資料庫交易記錄 (.log)
    
    刪除交易記錄時 (由於透過備份或循環記錄而截斷)，沒有任何程序可將 NTFS 檔案系統中儲存已刪除之記錄檔的區塊清空。NTFS 有可能會快速重複利用該可用空間來儲存新建立的記錄，但是不保證這一定會發生。

  - 內容索引類別目錄檔案
    
    Exchange 2013 使用 Search Foundation 來執行搜尋檢索功能。搜尋索引類別目錄是由幾十個檔案組成，這些檔案與信箱資料庫檔案儲存在相同的磁碟區中。從信箱資料庫實刪除郵件時，不會立即刪除搜尋類別目錄中關聯的內容。當 Search Foundation 執行陰影或主要合併將許多小型類別目錄檔案合併成單一較大檔案時，便會刪除內容。完成主要合併後，便會將較小的類別目錄檔案刪除。沒有任何程序可將儲存已刪除之類別目錄檔案的區塊清空。

