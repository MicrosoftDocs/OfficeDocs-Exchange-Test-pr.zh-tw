---
title: '郵件追蹤: Exchange 2013 Help'
TOCTitle: 郵件追蹤
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 51409209
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 郵件追蹤

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

在 Microsoft Exchange Server 2013 中，郵件追蹤記錄檔會在信箱伺服器上的傳輸服務、信箱伺服器上的信箱和邊緣傳輸伺服器上傳入及傳出郵件時詳細記錄所有的郵件活動。您可以使用郵件追蹤記錄檔進行郵件鑑識、郵件流程分析、報告及疑難排解等工作。

在 Exchange 2013 中，因為 Exchange 2013 信箱伺服器含有傳輸服務與信箱，所以您可以使用 **Set-TransportService** Cmdlet 或 **Set-MailboxServer** Cmdlet 進行所有的郵件追蹤組態工作。您可以使用其中一項 Cmdlet，進行下列郵件追蹤組態變更：

  - 啟用或停用郵件追蹤。預設值是啟用。

  - 指定郵件追蹤記錄檔的位置。

  - 指定個別郵件追蹤記錄檔的大小上限。預設值是 10 MB。

  - 指定含有郵件追蹤記錄檔之目錄的大小上限：預設值為 1000 MB。

  - 指定郵件追蹤記錄檔的保留天數上限：預設為 30 天。

  - 啟用或停用郵件追蹤記錄檔中的郵件主旨記錄。預設值是啟用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以使用 Exchange 系統管理中心 (EAC) 來啟用或停用郵件追蹤，以及指定郵件追蹤記錄檔的位置。</td>
</tr>
</tbody>
</table>


Exchange 預設會根據檔案大小及檔案保留天數，使用循環記錄來限制郵件追蹤記錄檔，以助控制郵件追蹤記錄檔所使用的硬碟空間。

**目錄**

搜尋郵件追蹤記錄檔

郵件追蹤記錄檔的結構

郵件追蹤記錄檔中的欄位

郵件追蹤記錄檔中的事件類型

郵件追蹤記錄檔中的來源值

郵件追蹤記錄檔中的範例項目

郵件追蹤記錄的安全性考量

## 搜尋郵件追蹤記錄檔

隨著郵件在 Exchange 2013 信箱伺服器中移動，郵件追蹤記錄檔會包含大量資料。若要搜尋郵件追蹤記錄檔，您有不同的選項可以使用。

  - **Get-MessageTrackingLog**   系統管理員可使用此 Cmdlet，透過各種篩選準則來搜尋郵件追蹤記錄檔中的郵件相關資訊。如需詳細資訊，請參閱＜[搜尋郵件追蹤記錄檔](search-message-tracking-logs-exchange-2013-help.md)＞。

  - **系統管理員適用的傳遞回報**   系統管理員可使用 Exchange 系統管理中心 (EAC) 的 **\[傳遞回報\]** 索引標籤，或使用基礎的 **Search-MessageTrackingReport** 與 **Get-MesageTrackingReport** Cmdlet，在郵件追蹤記錄檔中搜尋組織中的特定信箱所傳送或接收之郵件的相關資訊。如需詳細資訊，請參閱＜[系統管理員的傳遞回報](delivery-reports-for-administrators-exchange-2013-help.md)＞。

  - **使用者的傳遞回報**   使用者可使用 Outlook Web App 中的 **\[傳遞回報\]** 索引標籤，在郵件追蹤記錄檔中搜尋其本身的信箱所接收或傳送之郵件的相關資訊。如需詳細資訊，請參閱＜[使用者的傳遞回報](https://go.microsoft.com/fwlink/?linkid=279920)＞。

回到頁首

## 郵件追蹤記錄檔的結構

郵件追蹤記錄檔預設位於 %ExchangeInstallPath%TransportRoles\\Logs\\MessageTracking。

在郵件追蹤記錄檔目錄中，記錄檔的命名慣例為 `MSGTRK`*yyyymmdd-nnnn*`.log`、`MSGTRKMA`*yyyymmdd-nnnn*`.log`、`MSGTRKMD`*yyyymmdd-nnnn*`.log` 與 `MSGTRKMS`*yyyymmdd-nnnn*`.log`。不同的記錄檔分別供下列服務使用：

  - **MSGTRK**   這些記錄檔與傳輸服務相關聯。

  - **MSGTRKMA**   這些記錄檔與仲裁的傳輸所使用的核准與拒絕相關聯。如需詳細資訊，請參閱＜[管理郵件核准](manage-message-approval-exchange-2013-help.md)＞。

  - **MSGTRKMD**   這些記錄檔與「信箱傳輸傳遞」服務傳遞至信箱的郵件相關聯。

  - **MSGTRKMS**   這些記錄檔與「信箱傳輸提交」服務從信箱傳送出去的郵件相關聯。

記錄檔名稱中的預留位置代表下列資訊：

  - 預留位置 *yyyymmdd* 是依 Coordinated Universal Time (UTC) 時間為準的記錄檔建立日期。*yyyy* = 年、*mm* = 月，以及 *dd* = 日。

  - 針對每個郵件追蹤記錄檔名稱前置詞，預留位置 *nnnn* 是每天都從 1 開始的執行個體號碼。

資訊會寫入每個記錄檔中，直到檔案大小達到每個記錄檔的最大指定值為止。此時會開啟具有遞增之執行個體編號的新記錄檔。這個程序會在一天當中不斷地重複。當下列其中一種情況發生時，記錄檔輪替功能就會刪除最舊的記錄檔：

  - 記錄檔達到指定的保留天數上限。

  - 郵件追蹤記錄檔目錄達到指定的大小上限。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>郵件追蹤記錄檔目錄的大小上限，是以擁有相同名稱前置詞之所有記錄檔的總大小來計算。其他不遵循名稱前置詞慣例的檔案，並不會納入總目錄大小的計算。將舊的記錄檔重新命名或將其他檔案複製到郵件追蹤記錄檔目錄中，可能會導致該目錄超過其指定的大小上限。<br />
    在 Exchange 2013 信箱伺服器上，郵件追蹤記錄檔目錄的大小上限為指定值的三倍。雖然由這四種不同的服務所產生的郵件追蹤記錄檔有四種不同的名稱前置詞，但寫入至 <strong>MSGTRKMA</strong> 的資料數量與頻率，相較於其他三種記錄檔前置詞而言顯得微不足道。</td>
    </tr>
    </tbody>
    </table>


郵件追蹤記錄檔是包含逗號分隔值 (CSV) 格式之資料的文字檔。每個郵件追蹤記錄檔都有包含下列資訊的標頭：

  - **\#Software：**郵件追蹤記錄檔的建立軟體名稱。一般情況下，這個值是 Microsoft Exchange Server。

  - **\#Version：**郵件追蹤記錄檔的建立軟體版本號碼。目前這個值為 15.0.0.0。

  - **\#Log-Type：**記錄類型值，即 Message Tracking Log。

  - **\#Date：**   建立記錄檔的 UTC 日期時間。以 ISO 8601 日期時間格式表示 UTC 日期時間：*yyyy-mm-dd*T*hh:mm:ss.fff*Z，其中 *yyyy* = 年、*mm* = 月、*dd* = 日，T 表示時間元件的開頭，*hh* = 時、*mm* = 分、*ss* = 秒、*fff* = 秒的分數，以及另外一個表示 UTC 的方法 Z 代表 Zulu。

  - **\#Fields：**郵件追蹤記錄檔中所使用的以逗號分隔欄位名稱。

回到頁首

## 郵件追蹤記錄檔中的欄位

郵件追蹤記錄檔會在記錄中將每個郵件事件儲存成一行。郵件事件資訊會以欄位來組織，而這些欄位會以逗號分隔。欄位名稱通常具有足夠的描述資訊，可用以判斷其內含的資訊類型。但有些欄位可能會空白，或者，儲存在欄位中的資訊類型，可能會根據郵件事件類型以及記錄了該事件的郵件追蹤記錄檔的類型而變更。下表提供將每個郵件追蹤事件進行分類時所使用欄位的一般描述。


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
<td><p><strong>date-time</strong></p></td>
<td><p>郵件追蹤事件的 UTC 日期時間。以 ISO 8601 日期時間格式表示 UTC 日期時間：<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z，其中 <em>yyyy</em> = 年、<em>mm</em> = 月、<em>dd</em> = 日，T 表示時間元件的開頭，<em>hh</em> = 時、<em>mm</em> = 分、<em>ss</em> = 秒、<em>fff</em> = 秒的分數，以及另外一個表示 UTC 的方法 Z 代表 Zulu。</p></td>
</tr>
<tr class="even">
<td><p><strong>client-ip</strong></p></td>
<td><p>將郵件提交之郵件伺服器或郵件用戶端的 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>client-hostname</strong></p></td>
<td><p>將郵件提交之郵件伺服器或郵件用戶端的主機名稱或 FQDN。</p></td>
</tr>
<tr class="even">
<td><p><strong>server-ip</strong></p></td>
<td><p>來源或目的地 Exchange 伺服器的 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>server-hostname</strong></p></td>
<td><p>目的地伺服器的主機名稱或 FQDN。</p></td>
</tr>
<tr class="even">
<td><p><strong>source-context</strong></p></td>
<td><p>與 <strong>source</strong> 欄位相關聯的額外資訊。例如，傳輸代理程式資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>connector-id</strong></p></td>
<td><p>來源或目的地「傳送」連接器或「接收」連接器的名稱。例如 <em>ServerName</em>\<em>ConnectorName</em> 或 <em>ConnectorName</em>。</p></td>
</tr>
<tr class="even">
<td><p><strong>source</strong></p></td>
<td><p>負責處理郵件追蹤事件的 Exchange 傳輸元件。此欄位中的值將在本主題稍後的郵件追蹤記錄檔中的來源值一節中說明。</p></td>
</tr>
<tr class="odd">
<td><p><strong>event-id</strong></p></td>
<td><p>郵件事件類型。事件類型將在本主題稍後的郵件追蹤記錄檔中的事件類型一節中說明。</p></td>
</tr>
<tr class="even">
<td><p><strong>internal-message-id</strong></p></td>
<td><p>由目前處理郵件的 Exchange 伺服器所指派的郵件識別碼。</p>
<p>在參與郵件傳輸的每部 Exchange 伺服器的郵件追蹤記錄檔中，特定郵件的 <strong>internal-message-id</strong> 值是不同的。例如，此值可能為 <code>73014444033</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-id</strong></p></td>
<td><p>郵件標頭中 <strong>Message-Id:</strong> 標頭欄位的值。如果 <strong>Message-Id:</strong> 標頭欄位不存在或空白，則會指派任意值。此值是郵件存留時間的常數。若是在 Exchange 中建立的郵件，此值會採用 <code>&lt;GUID@ServerFQDN&gt;</code> 的格式，包括角括弧 (<code>&lt; &gt;</code>)。例如，<code>&lt;4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com&gt;</code>。其他郵件系統可能會使用不同的語法或值。</p></td>
</tr>
<tr class="even">
<td><p><strong>network-message-id</strong></p></td>
<td><p>唯一的郵件識別碼值，會持續存在於郵件所有因為複本發送或通訊群組展開等原因而產生的副本上。例如，此值可能為 <code>1341ac7b13fb42ab4d4408cf7f55890f</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>recipient-address</strong></p></td>
<td><p>郵件收件者的電子郵件地址。多個電子郵件地址會以分號字元 (;) 隔開。</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-status</strong></p></td>
<td><p>此欄位包含每個收件者的收件者狀態，並以分號字元 (;) 隔開。收件者狀態值的顯示順序與 <strong>recipient-address</strong> 欄位中的值順序相同。範例狀態值包括 <code>250 2.1.5 Recipient OK</code> 或 <code>550 4.4.7 QUEUE.Expired;&lt;ErrorText&gt;</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>total-bytes</strong></p></td>
<td><p>含附件的郵件大小，以位元組為單位。</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-count</strong></p></td>
<td><p>郵件中的收件者數目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>related-recipient-address</strong></p></td>
<td><p><strong>EXPAND</strong>、<strong>REDIRECT</strong> 與 <strong>RESOLVE</strong> 事件會使用此欄位，顯示與郵件相關聯的其他收件者電子郵件地址。</p></td>
</tr>
<tr class="even">
<td><p><strong>reference</strong></p></td>
<td><p>此欄位包含特定事件類型的其他資訊。例如：</p>
<p><strong>DSN</strong>   包含報告連結；如果在此事件之後產生了傳遞狀態通知 (DSN)，即為相關聯 DSN 的 <strong>Message-Id</strong> 值。如果這是 DSN 郵件，則 <strong>Reference</strong> 欄位會包含此 DNS 所針對之原始郵件的 <strong>Message-Id</strong> 值。</p>
<p><strong>EXPAND</strong>   [參考] 欄位包含相關郵件的 <strong>related-recipient-address</strong> 值。</p>
<p><strong>RECEIVE</strong>   如果郵件是由其他程序 (例如日誌或收件匣規則) 所產生，則 [參考] 欄位可能會包含相關郵件的 <strong>Message-Id</strong> 值。</p>
<p><strong>SEND</strong>   [參考] 欄位包含任何 DSN 郵件的 <strong>Internal-Message-Id</strong> 值。</p>
<p><strong>THROTTLE</strong>   [參考] 欄位包含郵件受到節流的原因。</p>
<p><strong>TRANSFER</strong>   此參考欄位包含分支之郵件的 Internet-Message-Id。</p>
<p>對於由收件匣規則產生的郵件，[<strong>Reference</strong>] 欄位包含當初導致收件匣規則產生輸出郵件的輸入郵件的 <strong>Internal-Message-Id</strong> 值。</p>
<p>對於其他類型的事件，[<strong>Reference</strong>] 欄位可能會包含遭分支之郵件的 <strong>Internal-Message-Id</strong> 值。</p>
<p>對於其他類型的事件，[<strong>Reference</strong>] 欄位通常為空白。</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-subject</strong></p></td>
<td><p>在 <code>Subject:</code> 標頭欄位中找到的郵件主旨。郵件主旨的追蹤是由 <strong>Set-TransportService</strong> 或 <strong>Set-MailboxServer</strong> Cmdlet 中的 <em>MessageTrackingLogSubjectLoggingEnabled</em> 參數來控制。預設會啟用郵件主旨追蹤。</p></td>
</tr>
<tr class="even">
<td><p><strong>sender-address</strong></p></td>
<td><p>在 <code>Sender:</code> 標頭欄位或 <code>From:</code> 標頭欄位 (如果 <code>Sender:</code> 不存在) 中指定的電子郵件地址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>return-path</strong></p></td>
<td><p>由郵件信封中的 <code>MAIL FROM:</code> 指定的退回電子郵件地址。雖然此欄位絕對不會是空白，但會以 <code>&lt;&gt;</code> 來表示 Null 寄件者地址值。</p></td>
</tr>
<tr class="even">
<td><p><strong>message-info</strong></p></td>
<td><p>郵件的其他相關資訊。例如：</p>
<ul>
<li><p><strong>DELIVER</strong> 與 <strong>SEND</strong> 事件的郵件原始 UTC 日期時間。原始日期時間是指郵件最初進入 Exchange 組織的時間。以 ISO 8601 日期時間格式表示 UTC 日期時間：<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z，其中 <em>yyyy</em> = 年、<em>mm</em> = 月、<em>dd</em> = 日，T 表示時間元件的開頭，<em>hh</em> = 時、<em>mm</em> = 分、<em>ss</em> = 秒、<em>fff</em> = 秒的分數，以及另外一個表示 UTC 的方法 Z 代表 Zulu。</p></li>
<li><p>驗證錯誤。例如，您可能會看見值 <code>11a</code>，以及發生驗證錯誤時所使用的驗證類型。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>directionality</strong></p></td>
<td><p>郵件的方向。範例值包括 <code>Incoming</code>、<code>Undefined</code> 與 <code>Originating</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>tenant-id</strong></p></td>
<td><p>內部部署 Exchange 2013 組織中不會使用此欄位。</p></td>
</tr>
<tr class="odd">
<td><p><strong>original-client-ip</strong></p></td>
<td><p>原始用戶端的 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>original-server-ip</strong></p></td>
<td><p>原始伺服器的 IPv4 或 IPv6 位址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>custom-data</strong></p></td>
<td><p>此欄位包含特定事件類型的相關資料。例如，「傳輸規則」代理程式會使用此欄位，針對對郵件執行了動作的傳輸規則或 DLP 原則，記錄其 GUID。如需這些「傳輸規則」代理程式值的詳細資訊，請參閱 <a href="view-dlp-policy-detection-reports-exchange-2013-help.md">檢視 DLP 原則偵測報告</a>主題中的「資料記錄」一節。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 郵件追蹤記錄檔中的事件類型

**event-id** 欄位中的各種事件類型可用來將郵件追蹤記錄檔中的郵件事件分類。有些郵件事件只會出現在一種類型的郵件追蹤記錄檔中，有些郵件事件則會出現在所有類型的郵件追蹤記錄檔中。下表說明用以分類每個郵件事件的事件類型。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AGENTINFO</strong></p></td>
<td><p>傳輸代理程式會使用此事件來記錄自訂資料。</p></td>
</tr>
<tr class="even">
<td><p><strong>BADMAIL</strong></p></td>
<td><p>由「收取」目錄或「重新顯示」目錄所提交，但無法傳遞或遭退回的郵件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DEFER</strong></p></td>
<td><p>郵件傳遞延遲。</p></td>
</tr>
<tr class="even">
<td><p><strong>DELIVER</strong></p></td>
<td><p>郵件已傳遞至本機信箱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DROP</strong></p></td>
<td><p>已捨棄郵件，而不需要傳遞狀態通知 (也稱為 DSN、退回的郵件、未傳遞回報或 NDR)。例如：</p>
<ul>
<li><p>已完成的仲裁核准要求郵件。</p></li>
<li><p>以無訊息方式捨棄的垃圾郵件 (沒有 NDR)。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>已產生傳遞狀態通知 (DSN)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEDELIVER</strong></p></td>
<td><p>重複的郵件已傳遞給收件者。如果收件者是多個巢狀通訊群組的成員，可能會出現郵件重複情形。資訊儲存庫會偵測到重複的郵件並加以移除。</p></td>
</tr>
<tr class="even">
<td><p><strong>DUPLICATEEXPAND</strong></p></td>
<td><p>在通訊群組展開期間，偵測到重複的收件者。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEREDIRECT</strong></p></td>
<td><p>郵件的替代收件者已是收件者。</p></td>
</tr>
<tr class="even">
<td><p><strong>EXPAND</strong></p></td>
<td><p>已展開通訊群組。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FAIL</strong></p></td>
<td><p>郵件傳遞失敗。來源包括 <strong>SMTP</strong>、<strong>DNS</strong>、<strong>QUEUE</strong> 與 <strong>ROUTING</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>HADISCARD</strong></p></td>
<td><p>在將主要複本傳遞至下一個躍點之後，已捨棄陰影郵件。如需詳細資訊，請參閱＜<a href="shadow-redundancy-exchange-2013-help.md">陰影備援</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HARECEIVE</strong></p></td>
<td><p>本機資料庫可用性群組 (DAG) 中或 Active Directory 站台中的伺服器接收到陰影郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>HAREDIRECT</strong></p></td>
<td><p>已建立陰影郵件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HAREDIRECTFAIL</strong></p></td>
<td><p>無法建立陰影郵件。詳細資料會儲存在 <strong>source-context</strong> 欄位中。</p></td>
</tr>
<tr class="even">
<td><p><strong>INITMESSAGECREATED</strong></p></td>
<td><p>郵件已傳送給仲裁收件者，因此郵件已傳送至仲裁信箱進行核准。如需詳細資訊，請參閱＜<a href="manage-message-approval-exchange-2013-help.md">管理郵件核准</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LOAD</strong></p></td>
<td><p>已在開機時順利載入郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATIONEXPIRE</strong></p></td>
<td><p>仲裁收件者的仲裁者始終未核准或拒絕郵件，因此郵件已過期。如需仲裁收件者的詳細資訊，請參閱<a href="manage-message-approval-exchange-2013-help.md">管理郵件核准</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORAPPROVE</strong></p></td>
<td><p>仲裁收件者的仲裁者已核准郵件，因此郵件已傳遞給仲裁收件者。</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATORREJECT</strong></p></td>
<td><p>仲裁收件者的仲裁者已拒絕郵件，因此郵件未傳遞給仲裁收件者。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORSALLNDR</strong></p></td>
<td><p>對某個仲裁收件者的所有仲裁者傳送的所有核准要求皆無法傳遞，並且產生未傳遞回報 (NDR)。</p></td>
</tr>
<tr class="even">
<td><p><strong>NOTIFYMAPI</strong></p></td>
<td><p>在本機伺服器上某個信箱的寄件匣中偵測到郵件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NOTIFYSHADOW</strong></p></td>
<td><p>在本機伺服器上某個信箱的寄件匣中偵測到郵件，而必須建立郵件的陰影複本。</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>郵件已放入有害郵件佇列中，或是已從有害郵件佇列中移除。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PROCESS</strong></p></td>
<td><p>郵件處理成功。</p></td>
</tr>
<tr class="even">
<td><p><strong>PROCESSMEETINGMESSAGE</strong></p></td>
<td><p>信箱傳輸傳遞服務所處理的會議郵件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RECEIVE</strong></p></td>
<td><p>傳輸服務的 SMTP 接收元件已從「收取」或「重新顯示」目錄接收到郵件 (來源：<code>SMTP</code>)，或已從信箱提交郵件至「信箱傳輸提交」服務 (來源：<code>STOREDRIVER</code>)。</p></td>
</tr>
<tr class="even">
<td><p><strong>REDIRECT</strong></p></td>
<td><p>在 Active Directory 查閱之後，郵件已重新導向至替代收件者。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESOLVE</strong></p></td>
<td><p>在 Active Directory 查閱之後，郵件的收件者已解析為不同的電子郵件地址。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMIT</strong></p></td>
<td><p>已從 Safety Net 自動重新提交郵件。如需詳細資訊，請參閱 ＜<a href="safety-net-exchange-2013-help.md">安全網</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESUBMITDEFER</strong></p></td>
<td><p>從 Safety Net 重新提交的郵件發生延遲。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMITFAIL</strong></p></td>
<td><p>從 Safety Net 重新提交的郵件已失敗。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SEND</strong></p></td>
<td><p>傳輸服務之間已以 SMTP 傳送郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMIT</strong></p></td>
<td><p>「信箱傳輸提交」服務已順利將郵件傳送至「傳輸」服務。就 <strong>SUBMIT</strong> 事件而言，<strong>source-context</strong> 內容會包含下列詳細資料：</p>
<ul>
<li><p><strong>MDB</strong>   信箱資料庫 GUID。</p></li>
<li><p><strong>Mailbox</strong>   信箱 GUID。</p></li>
<li><p><strong>Event</strong>   事件序號。</p></li>
<li><p><strong>MessageClass</strong>   郵件的類型。例如，<code>IPM.Note</code>。</p></li>
<li><p><strong>CreationTime</strong>   提交郵件的日期和時間。</p></li>
<li><p><strong>ClientType</strong>   例如 <code>User</code>、<code>OWA</code> 或 <code>ActiveSync</code>。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>SUBMITDEFER</strong></p></td>
<td><p>從「信箱傳輸提交」服務到「傳輸」服務的郵件傳送作業發生延遲。</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMITFAIL</strong></p></td>
<td><p>從「信箱傳輸提交」服務到「傳輸」服務的郵件傳送作業已失敗。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SUPPRESSED</strong></p></td>
<td><p>已抑制郵件傳輸。</p></td>
</tr>
<tr class="even">
<td><p><strong>THROTTLE</strong></p></td>
<td><p>已將郵件進行節流。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TRANSFER</strong></p></td>
<td><p>由於內容轉換、郵件收件者限制或代理程式的緣故，收件者已移至分支的郵件。來源包括 <strong>ROUTING</strong> 或 <strong>QUEUE</strong>。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 郵件追蹤記錄檔中的來源值

在郵件追蹤記錄檔中，**source** 欄位的值可指出負責處理郵件追蹤事件的傳輸元件。下表說明 **source** 欄位的值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>來源值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ADMIN</strong></p></td>
<td><p>事件來源為人為干預。例如，系統管理員使用佇列檢視器刪除郵件，或使用「重新顯示」目錄提交郵件檔案。</p></td>
</tr>
<tr class="even">
<td><p><strong>AGENT</strong></p></td>
<td><p>事件來源為傳輸代理程式。</p></td>
</tr>
<tr class="odd">
<td><p><strong>APPROVAL</strong></p></td>
<td><p>事件來源為搭配仲裁收件者使用的核准架構。如需詳細資訊，請參閱＜<a href="manage-message-approval-exchange-2013-help.md">管理郵件核准</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>BOOTLOADER</strong></p></td>
<td><p>事件來源是開機時存在於伺服器上的未處理郵件。這與 <strong>LOAD</strong> 事件類型相關。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DNS</strong></p></td>
<td><p>事件來源為 DNS。</p></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>事件來源為傳遞狀態通知 (DSN)。例如未傳遞回報 (NDR)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GATEWAY</strong></p></td>
<td><p>事件來源為外部連接器。如需詳細資訊，請參閱＜<a href="foreign-connectors-exchange-2013-help.md">外部連接器</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>MAILBOXRULE</strong></p></td>
<td><p>事件來源為收件匣規則。如需詳細資訊，請參閱＜<a href="https://go.microsoft.com/fwlink/?linkid=285479">收件匣規則</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MEETINGMESSAGEPROCESSOR</strong></p></td>
<td><p>事件來源是會議郵件處理器，它會根據會議更新來更新行事曆。</p></td>
</tr>
<tr class="even">
<td><p><strong>ORAR</strong></p></td>
<td><p>事件來源為「發送者要求替代收件者」(ORAR)。您可以在 <strong>New-ReceiveConnector</strong> 或 <strong>Set-ReceiveConnector</strong> Cmdlet 上使用 <em>OrarEnabled</em> 參數，以在「接收」連接器上啟用或停用 ORAR 的支援。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PICKUP</strong></p></td>
<td><p>事件來源為「收取」目錄。如需詳細資訊，請參閱＜<a href="pickup-directory-and-replay-directory-exchange-2013-help.md">收取目錄和重新顯示] 目錄</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>事件來源為有害郵件識別碼。如需有害郵件與有害郵件佇列的詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>PUBLICFOLDER</strong></p></td>
<td><p>事件來源為具有郵件功能的公用資料夾。</p></td>
</tr>
<tr class="even">
<td><p><strong>QUEUE</strong></p></td>
<td><p>事件來源為佇列。</p></td>
</tr>
<tr class="odd">
<td><p><strong>REDUNDANCY</strong></p></td>
<td><p>事件來源為陰影備援。如需詳細資訊，請參閱＜<a href="shadow-redundancy-exchange-2013-help.md">陰影備援</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>ROUTING</strong></p></td>
<td><p>事件來源為「傳輸」服務中之分類程式的路由解析元件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SAFETYNET</strong></p></td>
<td><p>事件來源為 Safety Net。如需詳細資訊，請參閱＜<a href="safety-net-exchange-2013-help.md">安全網</a>＞。</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP</strong></p></td>
<td><p>郵件已由傳輸服務的 SMTP 傳送元件或 SMTP 接收元件所提交。</p></td>
</tr>
<tr class="odd">
<td><p><strong>STOREDRIVER</strong></p></td>
<td><p>事件來源為本機伺服器上某個信箱中的 MAPI 提交。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 郵件追蹤記錄檔中的範例項目

在兩個使用者之間傳送未引發事件的郵件時，會在郵件追蹤記錄檔中產生數個項目。您可以使用 **Get-MessageTrackingLog** Cmdlet 來查看結果。如需詳細資訊，請參閱＜[搜尋郵件追蹤記錄檔](search-message-tracking-logs-exchange-2013-help.md)＞。

以下是當使用者 chris@contoso.com 順利將測試郵件傳送給使用者 michelle@contoso.com 時，所建立之郵件追蹤記錄項目的範例節錄。這兩名使用者在同一部伺服器上都有信箱。

    EventId    Source      Sender            Recipients             MessageSubject
    -------    ------      ------            ----------             --------------
    NOTIFYMAPI STOREDRIVER                   {}
    RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
    RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
    AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
    SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
    DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test

回到頁首

## 郵件追蹤記錄的安全性考量

郵件追蹤記錄檔中不會儲存郵件內容。依預設，郵件追蹤記錄檔中會儲存電子郵件的主旨行。為了滿足日益提高的安全性或隱私權需求，您可能想停用郵件主旨記錄。啟用或停用郵件主旨記錄前，請務必確認您組織中有關公開主旨列資訊的相關原則。如需詳細資訊，請參閱＜[設定郵件追蹤](configure-message-tracking-exchange-2013-help.md)＞。

回到頁首

