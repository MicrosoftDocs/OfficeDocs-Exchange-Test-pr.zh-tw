---
title: '背壓: Exchange 2013 Help'
TOCTitle: 背壓
ms:assetid: 03003544-e802-4988-9427-5fc4da64dcb8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201658(v=EXCHG.150)
ms:contentKeyID: 52062511
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 背壓

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

背壓是一種系統資源，可監控存在於 Microsoft Exchange 2013 Mailbox Server 及 Edge Transport Server 的 Microsoft Exchange 傳輸服務。

Exchange 可偵測重要資源 (例如可用的硬碟空間和記憶體) 壓力過大的時間，並採取行動以嘗試防止服務無法使用。背壓可防止系統資源不堪負荷，而 Exchange 伺服器會嘗試先處理現有的郵件，再接受任何新郵件。當系統資源的使用量恢復正常水準時，Exchange 伺服器會逐漸恢復為正常運作，並開始重新接受新郵件。

在 Exchange 2013 中，當 Mailbox Server 或 Edge Transport Server 上的傳輸服務承受資源壓力時，會接受傳入的連線，但透過這些連線的內送郵件，會以較低的速率接收或遭到拒絕。當 SMTP 主機嘗試連線至處於資源壓力下的 Exchange 伺服器時，連線便會成功。不過，當主機發出 **MAIL FROM** 命令以提交郵件時，根據處於壓力下的資源而定，傳輸服務會延遲 **MAIL FROM** 命令的認可或拒絕連線。

**目錄**

Resources monitored

Actions taken by Exchange Transport when under resource pressure

Back pressure configuration options in the EdgeTransport.exe.config file

Back pressure logging information

## 監視的資源

使用背壓功能時，會監視下列系統資源：

  - 硬碟上用來儲存郵件佇列資料庫的可用空間。

  - 硬碟上用來儲存郵件佇列資料庫交易記錄的可用空間。

  - 記憶體中未認可的訊息佇列資料庫交易數。

  - EdgeTransport.exe 處理程序使用的記憶體。

  - 所有其他處理程序使用的記憶體。

  - 提交佇列中的郵件數。

Mailbox Server 或 Edge Transport Server 上每個受監視的系統資源都會套用下列三種資源使用量層級之一：

  - **一般**   資源未使用過度。伺服器會接受新的連線及郵件。

  - **中**   資源稍微使用過度。會對伺服器套用有限的背壓。可以傳送來自授權網域之寄件者的郵件。不過，根據處於壓力下的特定資源，伺服器使用垃圾郵件防堵來延遲伺服器回應，或拒絕從其他資源傳入的 **MAIL FROM** 命令。

  - **高**   資源嚴重使用過度。會套用完整背壓。所有郵件流程都會停止，而且伺服器會拒絕所有新的傳送的 **MAIL FROM** 命令。

下列幾節說明 Exchange 如何處理特定資源處於壓力下的狀況。

## 郵件佇列資料庫的可用硬碟空間

根據預設，郵件佇列資料庫儲存在 %ExchangeInstallPath%TransportRoles\\data\\Queue。Exchange 會監視此位置的硬碟空間使用量。會使用下列公式計算高硬碟空間使用量層級：

100 \* (*硬碟大小* - *固定常數*) / *硬碟大小*

*固定常數* 的值是 500 百萬位元組 (MB)。

此公式所得結果是以硬碟空間總用量的百分比表示。此公式所得結果一律會四捨五入為最接近的整數。根據預設，中硬碟使用量層級比高層級低 2%。根據預設，一般硬碟使用量層級比高層級低 4%。

回到頁首

## 郵件佇列資料庫交易記錄的可用硬碟空間

根據預設，郵件佇列資料庫交易記錄儲存在 %ExchangeInstallPath%TransportRoles\\data\\Queue。Exchange 會監視此位置的硬碟空間使用量。%ExchangeInstallPath%Bin\\EdgeTransport.exe.config 應用程式組態檔包含預設值為 384 MB 的 *DatabaseCheckPointDepthMax* 機碼。此機碼會控制硬碟上之所有未認可交易記錄的總允許大小。此機碼會用在計算硬碟使用量的公式中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>DatabaseCheckPointDepthMax</em> 機碼值會套用至存在於 Mailbox Server 或 Edge Transport Server 上所有與傳輸相關的可延伸儲存引擎 (ESE) 資料庫。這包括訊息佇列資料庫及 IP 篩選資料庫。</td>
</tr>
</tbody>
</table>


根據預設，會使用下列公式計算高硬碟使用量層級：

100 \* (*硬碟大小* - Min(5 GB，3\**DatabaseCheckPointDepthMax*)) / *硬碟大小*

此公式所得結果一律會四捨五入為最接近的整數。根據預設，中硬碟使用量層級比高層級低 2%。一般硬碟使用量層級比高層級低 4%。

回到頁首

## 記憶體中未認可的郵件佇列資料庫交易數

對訊息佇列資料庫進行的變更清單會保留在記憶體中，直到可以將這些變更認可到交易記錄為止。然後，這份清單就會認可至訊息佇列資料庫本身。這些保留在記憶體中的未完成訊息佇列資料庫交易稱為「版本桶 (bucket)」。版本 Bucket 的數目可能會因非預期的大量內送郵件、垃圾郵件攻擊、郵件佇列資料庫完整性問題或硬碟效能，而增加到異常高的層級。

當 Exchange 開始接收郵件，這些郵件會以批次方式組合在一起，然後依版本 Bucket 做準備。如果內送郵件有大型附件，可以分成多個批次。正在處理的這些批次，稱為*「批次點」*。未完成的批次點數目可超過設定的閾值，特別是有大型附件的非預期大量內送郵件。

當版本 Bucket 或批次點處於壓力下，Exchange 伺服器會對傳入的郵件延遲認可，開始節流傳入的連線。Exchange 會透過垃圾郵件防堵 (延遲 **MAIL FROM** 命令)，來降低輸入郵件流程的速率。如果資源壓力狀況繼續發生，Exchange 會逐漸增加垃圾郵件防堵延遲。資源使用情況回復到正常之後，Exchange 會逐漸開始降低認可延遲，並輕鬆進入正常操作。根據預設，當處於資源壓力下，Exchange 會開始延遲郵件認可 10 秒。如果資源持續處於壓力下，延遲會增加，遞增量為 5 秒 (最長為 55 秒)

Exchange 會保留版本 Bucket 和批次點資源使用情況的歷程記錄。如果資源使用情況沒有下降到特定數目的輪詢間隔之正常層級 (稱為歷程記錄深度)，Exchange 會停止垃圾郵件防堵延遲，並開始拒絕內送郵件，直到資源使用情況回到正常為止。依預設，版本 Bucket 和批次點的歷程記錄深度，分別為 10 和 300 個輪詢間隔。

回到頁首

## EdgeTransport.exe 處理程序所使用的記憶體

預設會使用下列公式計算 EdgeTransport.exe 處理程序使用的高記憶體使用量層級：

實體記憶體總計的 75% 或 1 TB (以較少者為準)

此計算不包含硬碟分頁檔中的可用虛擬記憶體，或是其他處理程序所使用的記憶體。此公式所得結果是以 EdgeTransport.exe 處理程序所使用之記憶體總用量的百分比表示。此公式所得結果一律會四捨五入為最接近的整數。

EdgeTransport.exe 檔案使用的中記憶體使用量層級，預設是以實體記憶體總計的 73%，或高層級值減去 2% 計算 (以較少者為準)。EdgeTransport.exe 檔案使用的一般層級記憶體使用量，預設是以實體記憶體總計的 71%，或高層級值減去 4% 計算 (以較少者為準)。

如果 EdgeTransport.exe 處理程序的記憶體使用量高於指定的一般層級，則會強制進行「垃圾收集」。垃圾收集是一種處理程序，會檢查記憶體中的未使用物件，並收回這些未使用物件所用的記憶體。

Exchange 會保留 EdgeTransport.exe 處理程序的記憶體使用率歷程記錄。如果使用率沒有下降到特定數目的輪詢間隔之正常層級 (稱為歷程記錄深度)，Exchange 會開始拒絕內送郵件，直到資源使用情況回到正常為止。依預設，EdgeTransport.exe 記憶體使用率的歷程記錄深度為 30 個輪詢間隔。

回到頁首

## 所有處理程序所使用的記憶體

所有處理程序使用的高記憶體使用量層級，預設是實體記憶體總計的 94%。此值不包含硬碟分頁檔中的可用虛擬記憶體。

達到指定的記憶體使用量層級時，會執行*「郵件凍結」*作業。郵件凍結會將記憶體中快取之佇列郵件的不必要元素移除。完整的郵件會快取在記憶體中，以提高效能。將佇列郵件的 MIME 內容從記憶體中移除後，因為會直接從訊息佇列資料庫讀取郵件，所以可減少因耗用太多記憶體造成延遲變長的現象。預設會啟用郵件凍結。

回到頁首

## 提交佇列中的郵件數

提交佇列與 Exchange 2013 Mailbox Server 及 Edge Transport Server 上的傳輸服務相關聯。分類程式會處理提交佇列中的每一個郵件。此分類會導致郵件置於傳遞佇列中。如需詳細資訊，請參閱[郵件流程](mail-flow-exchange-2013-help.md)及[佇列](queues-exchange-2013-help.md)。提交佇列中若有大量郵件，表示分類程式在處理郵件時遇到困難。

當提交佇列處於壓力下，Exchange 伺服器會對傳入的郵件延遲認可，開始節流傳入的連線。Exchange 會透過垃圾郵件防堵 (延遲 **MAIL FROM** 命令)，來降低輸入郵件流程的速率。如果提交佇列壓力狀況繼續發生，Exchange 會逐漸增加垃圾郵件防堵延遲。提交佇列使用情況回復到正常之後，Exchange 會逐漸開始降低認可延遲，並輕鬆進入正常操作。根據預設，當處於提交佇列壓力下，Exchange 會開始延遲郵件認可 10 秒。如果提交佇列持續處於壓力下，延遲會增加，遞增量為 5 秒 (最長為 55 秒)。

Exchange 會保留提交佇列使用情況的歷程記錄。如果提交佇列使用情況沒有下降到特定數目的輪詢間隔之正常層級 (稱為歷程記錄深度)，Exchange 會停止垃圾郵件防堵延遲，並開始拒絕內送郵件，直到提交佇列使用情況回到正常為止。根據預設，提交佇列的歷程記錄深度為 300 個輪詢間隔。

## 資源壓力下 Exchange Transport 所採取的動作

下表總結特定資源處於壓力下時，Exchange 傳輸所採取的動作。

### 回應資源壓力時，Mailbox Server 及 Edge Transport Server 所採取的背壓動作

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>壓力下的資源</th>
<th>使用率層級</th>
<th>採取的動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>郵件佇列資料庫的硬碟空間</p></td>
<td><p>中型</p></td>
<td><ul>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>郵件佇列資料庫的硬碟空間</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>拒絕來自其他 Exchange 伺服器的內送郵件</p></li>
<li><p>透過 Mailbox Server 上的信箱傳輸提交服務拒絕來自信箱資料庫的郵件提交</p></li>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>郵件佇列資料庫交易記錄的硬碟空間</p></td>
<td><p>中型</p></td>
<td><ul>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>郵件佇列資料庫交易記錄的硬碟空間</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>拒絕來自其他 Exchange 伺服器的內送郵件</p></li>
<li><p>透過 Mailbox Server 上的信箱傳輸提交服務拒絕來自信箱資料庫的郵件提交</p></li>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>版本桶</p></td>
<td><p>中型</p></td>
<td><p>對內送郵件採用或遞增垃圾郵件防堵延遲。如果沒有達到整個版本 Bucket 歷程記錄深度的正常層級，請採取下列動作：</p>
<ul>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>版本桶</p></td>
<td><p>高</p></td>
<td><p>對內送郵件採用或遞增垃圾郵件防堵延遲。如果沒有達到整個版本 Bucket 歷程記錄深度的正常層級，請採取下列動作：</p>
<ul>
<li><p>拒絕來自其他 Exchange 伺服器的內送郵件</p></li>
<li><p>透過 Mailbox Server 上的信箱傳輸提交服務拒絕來自信箱資料庫的郵件提交</p></li>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>批次點</p></td>
<td><p>中型</p></td>
<td><p>對內送郵件採用或遞增垃圾郵件防堵延遲。如果沒有達到整個批次點歷程記錄深度的正常層級，請採取下列動作：</p>
<ul>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>批次點</p></td>
<td><p>高</p></td>
<td><p>對內送郵件採用或遞增垃圾郵件防堵延遲。如果沒有達到整個批次點歷程記錄深度的正常層級，請採取下列動作：</p>
<ul>
<li><p>拒絕來自其他 Exchange 伺服器的內送郵件</p></li>
<li><p>透過 Mailbox Server 上的信箱傳輸提交服務拒絕來自信箱資料庫的郵件提交</p></li>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>EdgeTransport.exe 處理程序所使用的記憶體</p></td>
<td><p>中型</p></td>
<td><ul>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
<li><p>強制廢棄項目回收</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe 處理程序所使用的記憶體</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>拒絕來自其他 Exchange 伺服器的內送郵件</p></li>
<li><p>透過 Mailbox Server 上的信箱傳輸提交服務拒絕來自信箱資料庫的郵件提交</p></li>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>所有處理程序所使用的記憶體</p></td>
<td><p>中型</p></td>
<td><ul>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
<li><p>強制廢棄項目回收</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>所有處理程序所使用的記憶體</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>拒絕來自其他 Exchange 伺服器的內送郵件</p></li>
<li><p>透過 Mailbox Server 上的信箱傳輸提交服務拒絕來自信箱資料庫的郵件提交</p></li>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
<li><p>從記憶體中清除加強的 DNS 快取</p></li>
<li><p>啟動郵件凍結</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>提交佇列中的郵件數</p></td>
<td><p>中型</p></td>
<td><p>對內送郵件採用或遞增垃圾郵件防堵延遲。如果沒有達到整個提交佇列歷程記錄深度的正常層級，請採取下列動作：</p>
<ul>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
<li><p>強制廢棄項目回收</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>提交佇列中的郵件數</p></td>
<td><p>高</p></td>
<td><p>對內送郵件採用或遞增垃圾郵件防堵延遲。如果沒有達到整個提交佇列歷程記錄深度的正常層級，請採取下列動作：</p>
<ul>
<li><p>拒絕來自其他 Exchange 伺服器的內送郵件</p></li>
<li><p>透過 Mailbox Server 上的信箱傳輸提交服務拒絕來自信箱資料庫的郵件提交</p></li>
<li><p>拒絕來自非 Exchange 伺服器的內送郵件</p></li>
<li><p>拒絕來自 Pickup 和 Replay 目錄的郵件提交</p></li>
<li><p>從記憶體中清除加強的 DNS 快取</p></li>
<li><p>啟動郵件凍結</p></li>
</ul></td>
</tr>
</tbody>
</table>


回到頁首

## EdgeTransport.exe.config 檔案中的背壓組態選項

背壓的所有組態選項都可在 %ExchangeInstallPath%Bin\\EdgeTransport.exe.config XML 應用程式組態檔中使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這些列出的設定僅供參考。強烈建議不要在 EdgeTransport.exe.config 檔案中對背壓設定做任何修改。修改背壓設定可能會導致效能不佳或資料遺失。建議您調查並修正所有可能發生的背壓事件之主要原因。</td>
</tr>
</tbody>
</table>


### 背壓組態選項

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機碼名稱</th>
<th>預設值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>EnableResourceMonitoring</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>ResourceMonitoringInterval</em></p></td>
<td><p><code>00:00:02</code> (2 秒)</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. 該值指出要使用的預設公式。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. 這個值表示實際值比 <em>PercentageDatabaseDiskSpaceUsedHighThreshold</em> 的值少 2%。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. 這個值表示實際值比 <em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em> 的值少 2%。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. 該值指出要使用的預設公式。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. 這個值表示實際值比 <em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em> 的值少 2%。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. 這個值表示實際值比 <em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em> 的值少 2%。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedHighThreshold</em></p></td>
<td><p>0. 此值表示會使用預設計算。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePrivateBytesUsedMediumThreshold</em></p></td>
<td><p>0. 這個值表示實際值比 <em>PercentagePrivateBytesUsedHighThreshold</em> 的值少 2%。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedNormalThreshold</em></p></td>
<td><p>0. 這個值表示實際值比 <em>PercentagePrivateBytesUsedMediumThreshold</em> 的值少 2%。</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsHighThreshold</em></p></td>
<td><p>200</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsMediumThreshold</em></p></td>
<td><p>120</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsNormalThreshold</em></p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsHistoryDepth</em></p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointHighThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointMediumThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointNormalThreshold</em></p></td>
<td><p>1000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointUseCostForPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointBatchSize</em></p></td>
<td><p>40</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointBatchTimeout</em></p></td>
<td><p><code>00:00:00.100</code> (0.1 秒)</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointItemExpiryInterval</em></p></td>
<td><p><code>00:05:00</code> (5 分鐘)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPBaseThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:00</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPMaxThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:55</code> (55 秒)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPStepThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:05</code> (5 秒)</p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPStartThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:10</code> (10 秒)</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePhysicalMemoryUsedLimit</em></p></td>
<td><p>94</p></td>
</tr>
<tr class="odd">
<td><p><em>DehydrateMessagesUnderMemoryPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateBytesHistoryDepth</em></p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueHighThreshold</em></p></td>
<td><p>10000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueMediumThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueNormalThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
</tbody>
</table>


回到頁首

## 背壓記錄資訊

下列清單描述 Exchange 中特定背壓事件所產生的事件日誌項目：

  - **資源使用量層級增加的事件日誌項目**
    
    事件類型：錯誤
    
    事件來源：MSExchangeTransport
    
    事件類別：資源管理員
    
    事件識別碼：15004
    
    描述：資源壓力從*之前的使用量層級*增加為*目前的使用量層級*。

  - **資源使用量層級減少的事件日誌項目**
    
    事件類型：參考
    
    事件來源：MSExchangeTransport
    
    事件類別：資源管理員
    
    事件識別碼：15005
    
    描述：資源壓力從*之前的使用量層級*減少為*目前的使用量層級*。

  - **可用磁碟空間嚴重不足的事件日誌項目**
    
    事件類型：錯誤
    
    事件來源：MSExchangeTransport
    
    事件類別：資源管理員
    
    事件識別碼：15006
    
    描述：Microsoft Exchange 傳輸服務正在拒絕郵件，因為可用磁碟空間低於設定的閾值。可能需要進行系統管理動作來釋放磁碟空間，讓服務繼續運作。

  - **可用記憶體嚴重不足的事件日誌項目**
    
    事件類型：錯誤
    
    事件來源：MSExchangeTransport
    
    事件類別：資源管理員
    
    事件識別碼：15007
    
    描述：Microsoft Exchange 傳輸服務正在拒絕郵件提交，因為服務持續耗用的記憶體超過設定的閾值。如此可能需要重新啟動此服務，以繼續正常運作。

回到頁首

