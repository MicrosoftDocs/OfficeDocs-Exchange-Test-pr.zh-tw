---
title: '優先順序佇列: Exchange 2013 Help'
TOCTitle: 優先順序佇列
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 51409189
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 優先順序佇列

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

*「優先佇列」(Priority Queuing)* 是 Exchange Server 2013 的一項功能，可啟用寄件者定義的郵件優先順序，以影響 Mailbox Server 的傳輸服務對郵件的處理方式。

寄件者會建立及傳送郵件時寄件者在 Microsoft Outlook 中指定郵件優先順序。寄件者可以在 Outlook 中設定下列任何一個郵件優先順序值：

  - 低重要性

  - 普通重要性

  - 高重要性

在 Outlook 或Outlook Web App中建立郵件的預設優先順序為一般優先順序。郵件優先順序會儲存在郵件標頭中的 \[ `X-Priority`標頭\] 欄位。

傳送或接收Exchange 2013組織中每封郵件必須在之前路由傳送，傳遞出的分類的信箱伺服器上的傳輸服務。信箱伺服器上的傳輸服務中分類程式提交佇列從一次挑選一個訊息而收件者的解決方式、 路由解析度和內容轉換對執行訊息之前放在傳遞佇列中的郵件。如需詳細資訊，請參閱[郵件流程](mail-flow-exchange-2013-help.md)。

傳遞佇列以動態方式建立根據郵件的目的地。如需詳細資訊，請參閱[佇列](queues-exchange-2013-help.md)。

具有相同的目的地的所有郵件是都放在相同的傳遞佇列中。優先順序佇列會影響傳遞佇列至目的地郵件伺服器的郵件的傳輸。啟用優先順序佇列時，高優先順序的郵件傳送到其目的地之前一般優先順序的郵件和一般優先順序的郵件傳送到其目的地之前低優先順序的郵件。優先順序的傳遞郵件優先順序為基礎的郵件可協助您的訊息傳遞時間定義特定的服務層次協議 (SLA) 需求。

## 用來設定優先佇列的選項

支援的優先順序佇列是由`%ExchangeInstallPath%bin\EdgeTransport.exe.config` XML 應用程式設定檔中的機碼所控制。如需如何設定優先順序佇列的指示，請參閱[啟用並設定優先順序佇列](enable-and-configure-priority-queuing-exchange-2013-help.md)。

下表將更詳細地說明每一個機碼。

### EdgeTransport.exe.config 檔案中的優先佇列機碼

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
<td><p><em>PriorityQueuingEnabled</em></p></td>
<td><p><code>false</code></p></td>
<td><p>此機碼啟用或停用 Mailbox server 上的傳輸服務中佇列的優先順序。此機碼的有效輸入是<code>true</code>或<code>false</code>。</p>
<p>這個機碼為 <code>false</code> 時，優先佇列會停用，將會忽略 EdgeTransport.exe.config 檔案中存在的所有優先佇列郵件限制。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxHighPriorityMessageSize</em></p></td>
<td><p><code>250KB</code></p></td>
<td><p>此索引鍵可指定允許的高優先順序的郵件大小上限。如果高優先順序郵件超過此索引鍵所指定的值，則郵件會自動從高優先順序降級至一般優先順序。</p>
<p>此機碼的值應該是大幅小於<strong>Set-TransportConfig</strong>指令程式上<em>MaxSendMessageSize</em>參數的值。此參數的預設值為<code>10 MB</code>。這兩個值的差異有助於確保高優先順序郵件一致且可預測的傳送時間。</p>
<p>當您輸入值時，請以下列其中一個單位來限定值：</p>
<ul>
<li><p>KB (千位元組)</p></li>
<li><p>MB (百萬位元組)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>LowPriorityDelayNotificationTimeout</em></p>
<p><em>NormalPriorityDelayNotificationTimeout</em></p>
<p><em>HighPriorityDelayNotificationTimeout</em></p></td>
<td><p><strong>低</strong>   <code>8:00:00</code> (8 小時)</p>
<p><strong>普通</strong>   <code>4:00:00</code> (4 小時)</p>
<p><strong>高</strong>   <code>00:30:00</code> (30 分鐘)</p></td>
<td><p>這些機碼會根據郵件優先順序，指定延遲傳遞狀態通知 (DSN) 郵件的逾時間隔。</p>
<p>每個郵件的傳遞失敗之後, 的傳輸服務會產生延遲 DSN 郵件和佇列以傳遞給無法傳遞郵件的寄件者。此延遲 DSN 郵件，則只有在指定的延遲通知逾時時間間隔之後已傳送且只有失敗的郵件未成功傳遞的時間。此延遲避免不必要的延遲時間可能會暫時郵件傳輸失敗所造成的 DSN 郵件的傳送。</p>
<p>若要指定值，請輸入時間範圍值：dd.hh:mm:ss，其中 d = 天數、h = 時數、m = 分鐘數，而 s = 秒數。</p></td>
</tr>
<tr class="even">
<td><p><em>LowPriorityMessageExpirationTimeout</em></p>
<p><em>NormalPriorityMessageExpirationTimeout</em></p>
<p><em>HighPriorityMessageExpirationTimeout</em></p></td>
<td><p><strong>低</strong>   <code>2.00:00:00</code> (2 天)</p>
<p><strong>普通</strong>   <code>2.00:00:00</code> (2 天)</p>
<p><strong>高</strong>   <code>8:00:00</code> (8 小時)</p></td>
<td><p>這些機碼指定傳輸服務嘗試失敗的訊息傳遞的時間的長度上限。如果之前到期逾時間隔通過無法成功傳遞郵件，便會包含原始郵件或訊息標頭未傳遞回報 (NDR) 傳遞給寄件者。</p>
<p>若要指定值，請輸入時間範圍值：dd.hh:mm:ss，其中 d = 天數、h = 時數、m = 分鐘數，而 s = 秒數。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPerDomainLowPriorityConnections</em></p>
<p><em>MaxPerDomainNormalPriorityConnections</em></p>
<p><em>MaxPerDomainHighPriorityConnections</em></p></td>
<td><p><strong>低</strong>   2</p>
<p><strong>普通</strong>   15</p>
<p><strong>高</strong>   3</p></td>
<td><p>這些機碼指定傳輸服務可以為任何單一的遠端網域已開啟的連線的數目上限。連至遠端網域發生使用傳遞佇列並傳送存在於信箱伺服器的連接器。</p>
<p>加總這些三個機碼應小於或等於<strong>Set-TransportService</strong>指令程式上<em>MaxPerDomainOutboundConnections</em>參數的值。此參數的預設值為<code>20</code>。</p></td>
</tr>
</tbody>
</table>


## 優先佇列如何影響 Mailbox Server 的其他郵件限制

通過傳輸服務的所有訊息都會受到各種訊息重試、 重新提交、 及到期時間限制。如需詳細資訊，請參閱[郵件大小限制](message-size-limits-exchange-2013-help.md)。

**Set-TransportService**指令程式提供一些郵件限制 EdgeTransport.exe.config 應用程式設定檔中有對應優先順序佇列中的郵件限制可用。下表顯示這些對應的郵件限制。

### Set-TransportService 指令程式中的郵件限制與 EdgeTransport.exe.config 檔案中對應的優先佇列郵件限制

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>來源</th>
<th>參數或機碼</th>
<th>預設值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code> (4 小時)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityDelayNotificationTimeout</em></p></td>
<td><p><code>4:00:00</code> (4 小時)</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MessageExpirationTimeOut</em></p></td>
<td><p><code>2.00:00:00</code> (2 天)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityMessageExpirationTimeout</em></p></td>
<td><p><code>2.00:00:00</code> (2 天)</p></td>
</tr>
</tbody>
</table>


當停用優先順序佇列時，會略過所有的優先順序佇列郵件限制存在於 EdgeTransport.exe.config 設定檔中。**Set-TransportService**指令程式上的所有郵件限制都套用至旅行社透過傳輸服務的 Mailbox server 的所有郵件。

啟用優先順序佇列時，佇列 EdgeTransport.exe.config 設定檔中的限制會覆寫相對應的郵件訊息的優先順序會限制**Set-TransportService** cmdlet 中。所有其他郵件限制**Set-TransportService** cmdlet 中仍適用於低優先順序、 一般優先順序，以及高優先順序的郵件通過傳輸服務的 Mailbox server。

## 優先佇列的使用者設定

**Set-Mailbox**指令程式具有*DowngradeHighPriorityMessagesEnabled*參數。預設值為`$false`。當此參數設為`$true`時，從信箱傳送任何高優先順序郵件會自動降級至一般優先順序。

