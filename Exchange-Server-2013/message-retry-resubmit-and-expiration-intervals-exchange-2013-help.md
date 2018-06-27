---
title: '郵件重試、 重新提交、 及到期時間間隔: Exchange 2013 Help'
TOCTitle: 郵件重試、 重新提交、 及到期時間間隔
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 51409150
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 郵件重試、 重新提交、 及到期時間間隔

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

在 Microsoft Exchange Server 2013、 無法成功傳遞的郵件只限根據郵件的來源和目的地的各種重試、 重新提交、 和到期期限。*重試*是已更新的連線嘗試與目的地。*重新提交*是法案回到來處理分類程式提交佇列傳送郵件。郵件*到期*後所有傳遞工作已都失敗一段指定時間。郵件到期後，傳遞失敗的通知寄件者。然後將郵件刪除佇列。

無論是重試、重新提交或過期，在自動處理郵件之前，您都可以先手動介入。

如需如何設定這些間隔的指示，請參閱[設定郵件重試、 重新提交、 及到期時間間隔](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md)。

## 郵件重試的組態選項

當傳輸伺服器無法連接至下一個躍點時，佇列就會處於 \[重試\] 狀態。系統會持續嘗試連線，直到佇列過期或連線建立為止。

## 自動郵件重試的組態選項

下表說明可用的郵件重試間隔組態選項。

### 可用的郵件重試間隔組態選項

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數或機碼名稱</th>
<th>預設值</th>
<th>設定位置</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>此機碼指定當傳輸伺服器無法連接至目的伺服器時，立即重試連線的次數。這種連線問題通常是由短暫的網路中斷所造成。</p>
<p>此機碼的有效輸入是 0 到 15 的整數。</p>
<p>除非網路不穩定，造成連線經常意外中斷，否則您通常不需要修改此機碼。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> 或 1 分鐘</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>此機碼控制 <em>QueueGlitchRetryCount</em> 機碼所指定的每個連線嘗試之間的連線間隔。</p>
<p>除非網路不穩定，造成連線經常意外中斷，否則您通常不需要修改此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p><strong>Set-TransportService</strong>指令程式或伺服器屬性中的 Exchange 系統管理中心 (EAC)</p></td>
<td><p>此參數指定在 <em>QueueGlitchRetryCount</em> 及 <em>QueueGlitchRetryInterval</em> 機碼所控制的連線嘗試失敗之後，重試連線的次數。 用盡 <em>QueueGlitchRetryCount</em> 及 <em>QueueGlitchRetryInterval</em> 機碼的連線問題，可能是由伺服器重新啟動或快取 DNS 查閱失敗所引起。</p>
<p>此參數的有效輸入是 0 到 15 的整數。如果將此參數設定為 0，則下個連線嘗試是由 <em>OutboundConnectionFailureRetryInterval</em> 參數所控制。</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Mailbox Server 上的傳輸服務： <code>00:05:00</code> 或 5 分鐘</p></li>
<li><p>Edge Transport Server： <code>00:01:00</code> 或 10 分鐘</p></li>
</ul></td>
<td><p>EAC 中的 <strong>Set-TransportService</strong> 指令程式或伺服器內容</p></td>
<td><p>此參數控制 <em>TransientFailureRetryCount</em> 參數所指定的每個連線嘗試之間的連線間隔。</p>
<p>若要指定值，請輸入時間範圍值：dd.hh:mm:ss，其中 d = 天數、h = 時數、m = 分鐘數，而 s = 秒數。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Mailbox Server 上的傳輸服務： <code>00:10:00</code> 或 10 分鐘</p></li>
<li><p>Edge Transport Server： <code>00:30:00</code> 或 30 分鐘</p></li>
</ul></td>
<td><p>EAC 中的 <strong>Set-TransportService</strong> 指令程式或伺服器內容</p></td>
<td><p>此參數指定當先前嘗試的輸出連線失敗時，重試連線的間隔。先前失敗的連線嘗試則是由 <em>TransientFailureRetryCount</em> 及 <em>TransientFailureRetryInterval</em> 參數控制。</p>
<p>若要指定值，請輸入時間範圍值：dd.hh:mm:ss，其中 d = 天數、h = 時數、m = 分鐘數，而 s = 秒數。</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> or15 分鐘</p></td>
<td><p><strong>Set-TransportService</strong> 指令程式</p></td>
<td><p>此參數指定當個別郵件的狀態為「重試」時，重試傳送該郵件的間隔。除非是有 Microsoft 客戶服務和支援的建議，否則建議您不要修改預設值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> 或 5 分鐘</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>此機碼指定佇列多久一次嘗試連線至信箱傳輸傳遞服務，以取得無法順利到達的目的地信箱資料庫。</p>
<p>若要指定值，請輸入時間範圍值：dd.hh:mm:ss，其中 d = 天數、h = 時數、m = 分鐘數，而 s = 秒數。</p>
<p>此機碼的有效輸入是 00:00:01 到 1.00:00:00。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 手動郵件重試的組態選項

當傳遞佇列處於「重試」狀態時，您可以使用 Exchange 工具箱中的佇列檢視器，或使用命令介面中的 **Retry-Queue** 指令程式，來手動強制立即嘗試連線。手動重試會覆寫下一個排定的重試時間。如果連線未成功，就會重設重試間隔計時器。傳遞佇列必須處於 \[重試\] 狀態，此動作才能生效。

如需詳細資訊，請參閱[管理佇列](manage-queues-exchange-2013-help.md)中的＜重試佇列＞一節。

回到頁首

## 延遲 DSN 郵件的組態選項

每次郵件傳遞失敗之後，Edge Transport Server 或 Mailbox Server 上的傳輸服務就會產生延遲的傳遞狀態通知 (DSN) 郵件並放在佇列中，以將它傳遞給無法傳遞郵件的寄件者。 此延遲的 DSN 郵件僅會在指定的延遲通知逾時間隔後，且失敗的郵件在這段時間仍然無法傳遞，才會傳送。 延遲通知逾時間隔預設為 4 小時。此項延遲可避免因暫時性的郵件傳輸失敗，而傳送不必要的延遲 DSN 郵件。 無論是 Exchange 組織內或組織外產生的郵件，都可以選擇性地啟用或停用傳送延遲 DSN 通知郵件。

下表說明延遲 DSN 通知郵件可用的組態選項。

### 延遲 DSN 通知郵件可用的組態選項

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數名稱</th>
<th>預設值</th>
<th>位置</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>4 小時</p></td>
<td><p>EAC 中的 <strong>Set-TransportService</strong> 或伺服器內容</p></td>
<td><p>此參數指定伺服器要等待多久之後才將延遲 DSN 郵件傳送給寄件者。該參數的值，應該永遠大於 <em>TransientFailureRetryCount</em> 參數的值乘以 <em>TransientFailureRetryInterval</em> 參數的值。</p>
<p>若要指定值，請輸入時間範圍值：dd.hh:mm:ss，其中 d = 天數、h = 時數、m = 分鐘數，而 s = 秒數。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>此參數指定延遲 DSN 郵件是否可以傳送給 Exchange 組織外的郵件寄件者。</p>
<p>這個參數的有效輸入是 <code>$true</code> 或 <code>$false</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>此參數指定延遲 DSN 郵件是否可以傳送給 Exchange 組織內的郵件寄件者。</p>
<p>這個參數的有效輸入是 <code>$true</code> 或 <code>$false</code>。</p></td>
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
<td>在 Exchange 2007 Hub Transport Server 上，所有 <em>ExternalDSN*</em> 及 <em>InternalDSN*</em> 參數都可在 <strong>Set-TransportServer</strong>指令程式上使用，但不能在 <strong>Set-TransportConfig</strong>指令程式上使用。 如果您的組織有任何 Exchange 2007 Hub Transport Server，則您需要在每一部 Exchange 2007 Hub Transport Server 上使用 <strong>Set-TransportServer</strong> 指令程式，來對這些值進行變更。</td>
</tr>
</tbody>
</table>


回到頁首

## 郵件重新提交的組態選項

郵件重新提交會將未傳遞郵件傳回提交佇列讓分類程式重新處理。

## 自動郵件重新提交

如果傳遞佇列處於 \[重試\] 狀態，而且無法在指定的時間內順利傳遞任何郵件，則會自動重新提交無法傳遞的郵件。 該時間是由 EdgeTransport.exe.config 應用程式組態檔中的 *MaxIdleTimeBeforeResubmit* 機碼所控制。 可自動重新提交的郵件僅限於傳遞佇列中的郵件。

若要指定值，請輸入時間範圍值：dd.hh:mm:ss，其中 d = 天數、h = 時數、m = 分鐘數，而 s = 秒數。

預設值為 `12:00:00` 或 12 小時。

## 手動重新提交郵件

您可以手動重新提交郵件信箱伺服器或 Edge Transport server 上的傳輸服務中具有下列狀態：

  - 具有「重試」狀態的傳遞佇列。佇列中的郵件必須不是處於「暫停」狀態。

  - 在「無法達到的」佇列中且不處於 \[已擱置\] 狀態的郵件。

  - 毒藥郵件佇列中的郵件。

如需毒藥郵件佇列和無法達到的佇列的詳細資訊，請參閱主題[佇列](queues-exchange-2013-help.md)中的＜關於毒藥郵件佇列及無法達到的佇列＞。

如果想要立即手動重新提交位於傳遞佇列或無法達到的佇列中的郵件，而不要再等待 *MaxIdleTimeBeforeResubmit* 參數所指定的時間經過，則您需要搭配使用 **Retry-Queue** 指令程式與 *Resubmit* 參數。若要手動重新提交毒藥郵件佇列中的郵件，您可以使用佇列檢視器或 **Resume-Message** 指令程式來繼續傳送郵件。 如需詳細資訊，請參閱[管理佇列](manage-queues-exchange-2013-help.md)中的＜重新提交佇列中的郵件＞一節。

手動重新提交郵件的另一種作法是擱置郵件、將郵件匯出成 .eml 副檔名的文字檔，然後將 .eml 檔案複製到任何 Mailbox Server 或 Edge Transport Server 上的重新顯示目錄。 此重新提交方法適用於位於傳遞佇列或無法達到的佇列中的郵件。毒藥郵件佇列中的郵件已處於 \[已擱置\] 狀態。「提交」佇列中的郵件則無法擱置或匯出。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>從佇列中匯出郵件時，不會從佇列中移除郵件。在匯出郵件並順利使用重新顯示目錄來重新提交郵件之後，應該移除擱置的郵件，以避免重複傳遞郵件。</td>
</tr>
</tbody>
</table>


如需詳細資訊，請參閱[從佇列匯出訊息](export-messages-from-queues-exchange-2013-help.md)。

回到頁首

## 郵件到期的組態選項

*訊息的到期逾時間隔*指定 Edge Transport server 或 Mailbox server 上的傳輸服務嘗試失敗的訊息傳遞的時間的長度上限。如果之前到期逾時間隔通過無法成功傳遞郵件，便會包含原始郵件或訊息標頭 NDR 傳遞給寄件者。

## 自動郵件到期

郵件到期逾時間隔是由 **Set-TransportService**指令程式中或 EAC 伺服器內容中的 *MessageExpirationTimeOut* 參數所控制。

若要指定值，請輸入時間範圍值：dd.hh:mm:ss，其中 d = 天數、h = 時數、m = 分鐘數，而 s = 秒數。

預設值為 `2.00:00:00` 或 2 天。此參數的有效輸入範圍是 `00:00:05` 到 `90.00:00:00`。

## 手動讓郵件到期

雖然無法手動強制讓郵件到期，但您可以手動從任何佇列中移除含或不含 NDR 的郵件，但「提交」佇列除外。

如需詳細資訊，請參閱[管理佇列中的郵件](manage-messages-in-queues-exchange-2013-help.md)中的＜從佇列中移除郵件＞一節。

回到頁首

