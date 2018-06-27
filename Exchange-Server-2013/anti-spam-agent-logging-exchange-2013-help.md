---
title: '反垃圾郵件代理程式記錄: Exchange 2013 Help'
TOCTitle: 反垃圾郵件代理程式記錄
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 50474429
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 反垃圾郵件代理程式記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

代理程式記錄檔記錄所 Microsoft Exchange Server 2013中的特定反垃圾郵件代理程式郵件上執行的動作。只有下列代理程式可寫入代理程式記錄檔資訊：

  - 連線篩選代理程式

  - 內容篩選器代理程式

  - 邊際規則代理程式

  - 收件者篩選器代理程式

  - 寄件者篩選器代理程式

  - 寄件者識別碼代理程式

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>無法使用 Mailbox server 上的連線篩選代理程式與 Edge 規則代理程式。</td>
</tr>
</tbody>
</table>


代理程式記錄中寫入的資訊，會視 SMTP 事件以及對郵件執行的動作而定。

您可以在 Exchange 管理命令介面使用**Set-TransportService**指令程式來執行所有代理程式記錄檔設定工作。下列選項都可供代理程式記錄檔：

  - 啟用或停用代理程式記錄。預設會啟用。

  - 指定代理程式記錄檔的位置。 預設值是 %exchangeinstallpath%transportroles\\logs\\hub\\agentlog。

  - 指定個別的代理程式記錄檔的大小上限。預設大小為 10 mb (MB)。

  - 指定包含代理程式記錄檔之目錄的大小上限。預設大小為 250 MB。

  - 指定代理程式記錄檔的保留時間上限。預設存留期為 7 天。

Exchange 會使用循環記錄，限制代理程式記錄使用的檔案大小及檔案保留天數，以協助控制記錄檔所使用的硬碟空間。

**目錄**

Overview of transport agents

Structure of the agent log files

Information written to the agent log

Search the agent logs

## 傳輸代理程式的概觀

代理程式僅可於用來傳輸郵件通過信箱伺服器或 Edge Transport server 上的傳輸服務的 SMTP 命令順序中的特定時間點的郵件時採取動作。SMTP 命令順序這些存取點稱為*SMTP 事件*。每個代理程式有可以指派的優先順序值。不過，SMTP 必須一律中事件發生特定的順序。因此，代理程式優先順序 SMTP 事件而定。如果兩個代理程式可以在相同的 SMTP 事件期間處理一則訊息，具有最高優先順序的代理程式將會處理郵件第一次。

下表列出各 SMTP 事件 (依出現順序排列)，並列出每個 SMTP 事件中將資訊寫入代理程式記錄的代理程式 (依優先順序從高至低排列)。

### SMTP 事件 (依出現順序排列)，以及每個 SMTP 事件中將資訊寫入代理程式記錄的代理程式 (依優先順序排列)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>SMTP 事件</th>
<th>Agent</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>OnConnect</strong></p></td>
<td><p>連線篩選代理程式</p></td>
</tr>
<tr class="even">
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>連線篩選代理程式</p>
<p>寄件者篩選器代理程式</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnRcptCommand</strong></p></td>
<td><p>連線篩選代理程式</p>
<p>收件者篩選器代理程式</p></td>
</tr>
<tr class="even">
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>連線篩選代理程式</p>
<p>寄件者識別碼代理程式</p>
<p>寄件者篩選器代理程式</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>邊際規則代理程式</p>
<p>內容篩選器代理程式</p></td>
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
<td>無法使用 Mailbox server 上的連線篩選代理程式與 Edge 規則代理程式。</td>
</tr>
</tbody>
</table>


如需代理程式、SMTP 事件及代理程式優先順序的相關資訊，請參閱[傳輸代理程式](transport-agents-exchange-2013-help.md)。

回到頁首

## 代理程式記錄檔的結構

代理程式記錄位於 %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog。

代理程式記錄檔的命名慣例是 AGENTLOG*yyyymmdd-nnnn*。 記錄檔。預留位置表示下列資訊：

  - 版面配置區*yyyymmdd*是建立記錄檔的國際標準時間 (UTC) 日期。版面配置區*yyyy* = year， *mm* = 月和*dd* = 日。

  - 預留位置 *nnnn* 是每天都從 1 開始的執行個體號碼。

資訊寫入記錄檔之前的檔案大小到達其最大的指定的值，並開啟新的記錄檔有依遞增的執行個體數。重複此程序在一天。當代理程式記錄檔目錄達到指定的大小上限，或是在記錄檔達到其最大指定保留時間下限循環記錄會刪除最舊的記錄檔。

代理程式記錄檔為文字檔包含逗點分隔值 (CSV) 檔案格式的資料。每個代理程式記錄檔有標頭包含下列資訊：

  - **\#Software**  軟體所建立的代理程式記錄檔的名稱。一般而言，此值為 Microsoft Exchange Server。

  - **\#Version**  建立代理程式記錄檔的軟體版本號碼。目前的值是 15.0.0.0。

  - **\#Log-Type**   記錄類型值，即「代理程式記錄」。

  - **\#Date**  建立記錄檔時 UTC 的日期時間。以 ISO 8601 日期時間格式表示 UTC 日期時間：*yyyy-mm-dd*T*hh:mm:ss.fff*Z，其中 *yyyy* = 年、*mm* = 月、*dd* = 日，T 表示時間元件的開頭，*hh* = 時、*mm* = 分、*ss* = 秒、*fff* = 秒的分數，以及另外一個表示 UTC 的方法 Z 代表 Zulu。

  - **\#Fields**   代理程式記錄檔中所使用之以逗號分隔的欄位名稱。

回到頁首

## 寫入代理程式記錄檔的資訊

代理程式記錄檔會儲存在記錄檔在單一行上每個代理程式交易。儲存在每行上的資訊被依據的欄位。這些欄位用逗號隔開。欄位名稱是描述性通常不夠判斷其所包含的資訊的類型。但是，欄位的一些可能會是空白。或儲存欄位中的資訊類型可能會變更根據代理程式或代理程式所執行的郵件上的動作。下表說明用來分類每個代理程式交易的欄位。

### 用於分類各代理程式交易的欄位

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>欄位名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Timestamp</strong></p></td>
<td><p>UTC 的日期-時間的代理程式事件。以 ISO 8601 日期時間格式表示 UTC 日期時間：<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z，其中 <em>yyyy</em> = 年、<em>mm</em> = 月、<em>dd</em> = 日，T 表示時間元件的開頭，<em>hh</em> = 時、<em>mm</em> = 分、<em>ss</em> = 秒、<em>fff</em> = 秒的分數，以及另外一個表示 UTC 的方法 Z 代表 Zulu。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionId</strong></p></td>
<td><p>唯一 SMTP 工作階段的識別碼。此識別碼被表示為 16 位數的十六進位數字。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalEndpoint</strong></p></td>
<td><p>本機 IP 位址和連接埠號碼接受郵件。SMTP 工作階段一般會使用連接埠 25。</p></td>
</tr>
<tr class="even">
<td><p><strong>RemoteEndpoint</strong></p></td>
<td><p>IP 位址和連接埠號碼連線到此伺服器以將郵件傳遞的上一個 SMTP 伺服器。網際網路郵件通過 Edge Transport server 周邊網路中， <strong>RemoteEndpoint</strong> Mailbox server 上的代理程式記錄檔中的值會將 Edge Transport server 的 IP 位址。即使郵件傳輸的 SMTP 傳送伺服器所使用的連接埠號碼會超過 1024 亂數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnteredOrgFromIP</strong></p></td>
<td><p>先連線至 Exchange 組織，以將郵件傳遞的遠端 SMTP 伺服器的 IP 位址。Edge Transport server 上， <strong>RemoteEndpoint</strong>與<strong>EnteredOrgFromIP</strong>的值都相同。反垃圾郵件代理程式會使用的 IP 位址<strong>EnteredOrgFromIP</strong>中要檢查郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageId</strong></p></td>
<td><p><code>MessageID</code>標頭欄位的值。如果這個值是空白的 Exchange 傳輸伺服器會指派任意值，但僅如果接受郵件。指派值之後， <code>MessageID</code>值的郵件的存留期為常數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>P1FromAddress</strong></p></td>
<td><p>寄件者電子郵件地址中<code>MAIL FROM</code>郵件信封中指定。這個值用來傳輸 SMTP 郵件伺服器之間的郵件。此值做為比較<strong>P2FromAddresses</strong>來判斷是否是在郵件標頭中的寄件者地址的值。</p></td>
</tr>
<tr class="even">
<td><p><strong>P2FromAddresses</strong></p></td>
<td><p>在郵件標頭之 <code>From</code> 標頭欄位，或 <code>Sender</code> 標頭欄位中指定的寄件者電子郵件地址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recipient</strong></p></td>
<td><p>收件者的電子郵件地址。雖然原始郵件可能包含多個收件者，只有一個收件者會顯示每行代理程式記錄檔中。</p></td>
</tr>
<tr class="even">
<td><p><strong>NumRecipients</strong></p></td>
<td><p>原始郵件中的收件者總數。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agent</strong></p></td>
<td><p>萬一巨集指令的代理程式的名稱。可能的值如下：</p>
<ul>
<li><p>內容篩選器代理程式</p></li>
<li><p>收件者篩選器代理程式</p></li>
<li><p>寄件者篩選器代理程式</p></li>
<li><p>寄件者識別碼代理程式</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Event</strong></p></td>
<td><p>SMTP 事件由代理程式所採取動作。<strong>Event</strong>值取決於代理程式。本主題稍早的第一個表格說明 SMTP 事件提供給每位代理。<strong>Event</strong>的可能值如下：</p>
<ul>
<li><p>OnConnect</p></li>
<li><p>OnEndOfHeaders</p></li>
<li><p>OnEndOfData</p></li>
<li><p>OnMailCommand</p></li>
<li><p>OnRcptCommand</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Action</strong></p></td>
<td><p>在郵件代理程式所採取的動作。<strong>Action</strong>的可能值如下：</p>
<ul>
<li><p>AcceptMessage</p></li>
<li><p>DeleteMessage</p></li>
<li><p>DeleteRecipients</p></li>
<li><p>Disconnect</p></li>
<li><p>QuarantineMessage</p></li>
<li><p>QuarantineRecipients</p></li>
<li><p>RejectAuthentication</p></li>
<li><p>RejectCommand</p></li>
<li><p>RejectConnection</p></li>
<li><p>RejectMessage</p></li>
<li><p>RejectRecipients</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>SmtpResponse</strong></p></td>
<td><p>增強的 SMTP 回應，如 RFC 2034 所定義。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reason</strong></p></td>
<td><p>代理程式提供的動作原因。</p></td>
</tr>
<tr class="even">
<td><p><strong>ReasonData</strong></p></td>
<td><p>代理程式提供的動作詳細說明。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 搜尋代理程式記錄

您可以使用 **Get-AgentLog** 指令程式和 **Get-AntiSpamFilteringReport.ps1** 指令碼來搜尋代理程式記錄。

**Get-AntiSpamFilteringReport.ps1**指令碼位於`%ExchangeInstallPath%Scripts`。您需要在命令介面中執行指令碼從指令碼\] 資料夾。若要變更的 Scripts 資料夾您的位置命令介面中的，執行下列命令：

    Cd $env:ExchangeInstallPath\Scripts

若要在 Scripts 資料夾中執行指令碼，請使用下列語法：

    .\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]

如需關於使用指令碼的使用資訊，請執行下列命令：

    Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1

回到頁首

