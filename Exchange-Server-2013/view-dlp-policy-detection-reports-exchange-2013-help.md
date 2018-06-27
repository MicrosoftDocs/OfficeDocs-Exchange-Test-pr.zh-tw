---
title: '檢視 DLP 原則偵測報告: Exchange 2013 Help'
TOCTitle: 檢視 DLP 原則偵測報告
ms:assetid: 5c3f1cf6-d8c7-4d83-bb24-641ea9d50cbc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150520(v=EXCHG.150)
ms:contentKeyID: 50472305
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視 DLP 原則偵測報告

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-16_

資料遺失防護 (DLP) 原則偵測管理廣泛定義組織執行以識別、 調查及解決 DLP 原則違規的活動。若要管理事件，您需要存取識別項目已偵測到的 DLP 原則的資訊。此偵測資訊整合現有的 Microsoft Exchange Server 2013資料和記錄檔格式，讓您可以運用現有的豐富型系統的資料來管理您的郵件流程事件。

如需建立事件報告及單一原則偵測事件的詳細資訊，請參閱[建立 DLP 原則偵測附隨報告](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)。 如需郵件記錄的相關資訊，請參閱 [使用傳遞回報追蹤郵件](track-messages-with-delivery-reports-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013：DLP 是需要 Exchange 企業版用戶端存取授權 (CAL) 的高階功能。如需 CAL 和伺服器授權的詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 授權</a>。</td>
</tr>
</tbody>
</table>


## 稽核資訊

在 Exchange DLP 偵測管理與相關的資料已整合至郵件追蹤記錄檔，也稱為傳遞回報。功能重複使用大部分的系統中可用的現有記錄架構。針對包含了解的郵件追蹤記錄檔結構的一般資訊，請檢閱[了解郵件追蹤](message-tracking-exchange-2013-help.md)或[使用傳遞回報追蹤郵件](track-messages-with-delivery-reports-exchange-2013-help.md)中現有的內容。

傳遞回報是所有郵件活動的詳細資訊記錄訊息會傳送到與信箱伺服器執行的傳輸服務的電腦。郵件追蹤記錄檔可透過 Exchange 管理命令介面使用**Get-MessageTrackingLog**指令程式。DLP 資料已整合至現有的資料格式和慣例追蹤傳遞回報。

## 資料記錄格式

郵件追蹤記錄包含來自涉及處理郵件流程內容之代理程式的資料。 對於 DLP 而言，傳輸規則代理程式 (TRA) 是用來呼叫深入的郵件內容掃描，以及用來套用定義為 ETR 一部分的原則。 現有的 AgentInfo 事件是用來新增郵件追蹤記錄中的 DLP 相關項目。

代理程式名稱在 AgentInfo 事件中為 \[TRA\] 或 \[傳輸規則代理程式\]。 將會依描述套用至郵件之 DLP 程序的郵件來記錄單一 AgentInfo 事件。 郵件追蹤記錄項目欄位的 \[CustomData\] 欄位其中的 DLP 資料是由出現的傳輸規則代理程式所記錄。 此欄位可包含多個項目： 郵件中找到的每一個資料分類有一項資料分類與客戶資訊行，每一個套用至郵件的規則有一個規則行，以及每一個超過負載或執行時間閾值的規則有一個健全狀況監視行。

DLP 記錄項目的示例顯示在此處。 輸出已格式化以顯示新行之間分隔行中的字串。

來源： AGENT

EventId： AGENTINFO

CustomData： S:TRA=DC|dcid=41BFDBC6C9D811E0816A3CD34824019B|count=10|conf=77;

S:TRA=DC|dcid=C7ECCBA0CA0011E0B6C00B124924019B|count=3|conf=81;

S:TRA=CI|sndOverride=or|just=Business Reason;

S:TRA=CI|sndOverride=fp;

S:TRA=ETR|ruleId=FC2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=PrependSubject|action=Encrypt|sev=2|mode=audit|dcid=41BFDBC6C9D811E0816A3CD34824019B|sndOverride=or;

S:TRA=ETR|ruleId=AB2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=Encrypt|sev=1|mode=enabled|dcid=C7ECCBA0CA0011E0B6C00B124924019B|sndOverride=fp;

S:TRA=ETRP|ruleId=C27D21EECA0311E0BCB896154924019B|LoadW=200|LoadC=100|ExecW=5500|ExecC=200;

「傳輸規則代理程式」需要分組規則 ID、DLP 原則 ID (選用)、上次修改日期、動作、嚴重性、模式、偵測到的資料分類 (選用)，以及根據規則 ID (由記錄行中的 "TRA=ETR" 指示) 的寄件者覆寫 (選用)。 其也需要將資料分類 ID、計數，以及分類的信賴等級依分類名稱 (由記錄行中的 "TRA=DC" 指示) 分組。

其他分組包含資料分類 ID、寄件者置換 (選用)，以及根據用戶端 (由記錄行中的 "TRA=CI" 指示) 所偵測到之所有分類的資料分類 ID 的覆寫理由 (選用)。 「傳輸規則代理程式」也需要將規則 ID、載入牆上時間 (選用)、載入 CPU 時間 (選用)、執行牆上時間 (選用)，以及執行 CPU 時間 (選用) 依超過載入或執行牆上時間或 CPU 時間閾值 (由記錄行中的 "TRA=ETRP" 指定) 之所有規則的規則 ID 進行分組。

以下是資料欄位的完整清單。 MTL 中的所有資料為類型字串。 格式欄說明如何辨識郵件追蹤記錄中的每一個欄位。 選用欄位欄指定當規則相符時無法記錄哪些欄位。 DLP 特定欄顯示哪些欄位是專用於 DLP 功能。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>欄位名稱</strong></p></td>
<td><p><strong>描述</strong></p></td>
<td><p><strong>格式</strong></p></td>
<td><p><strong>選用欄位</strong></p></td>
<td><p><strong>DLP 專屬</strong></p></td>
</tr>
<tr class="even">
<td><p>TRA</p></td>
<td><p>傳輸規則代理程式；鍵入 AgentName</p></td>
<td><p>TRA=DC、 ETR、 CI 或 ETRP</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>DC</p></td>
<td><p>資料分類；鍵入 groupName</p></td>
<td><p>TRA=DC</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>ETR</p></td>
<td><p>交換傳輸規則；鍵入 groupName</p></td>
<td><p>TRA=ETR</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>CI</p></td>
<td><p>用戶端資訊，鍵入 groupName</p></td>
<td><p>TRA=CI</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>ETRP</p></td>
<td><p>交換傳輸規則效能；鍵入 groupName</p></td>
<td><p>TRA=ETRP</p></td>
<td><p>選用</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>dcid</p></td>
<td><p>資料分類的 ID</p></td>
<td><p>dcid=GUID</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>count</p></td>
<td><p>資料分類的計數</p></td>
<td><p>count=整數</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>conf</p></td>
<td><p>資料分類的信賴等級</p></td>
<td><p>conf = 整數 (%)</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>sndOverride</p></td>
<td><p>寄件者覆寫；該欄位是可選的。</p>
<p>在 TRA=CI 行中，當欄位設為 &quot;or&quot; 表示資料分類已覆寫。 如果欄位設為 &quot;fp&quot; 表示資料分類已回報為誤判。</p>
<p>在 TRA=ETR 行中，當欄位設為 &quot;or&quot; 表示規則或部分規則已覆寫。 如果欄位設為 &quot;fp&quot; 表示規則或部分規則已回報為誤判。</p></td>
<td><p>sndOverride=or 或 fp</p>
<p>其中 &quot;or&quot; 代表覆寫，而 &quot;fp&quot; 代表誤判。 當使用者已針對規則回報覆寫或誤判時，會顯示 sndOverride 欄位。</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>just</p></td>
<td><p>理由；此欄位是可選的，而且只有在寄件人覆寫欄位在 TRA=CI 行中等於 &quot;or&quot; 時才可使用。 理由文字是由使用者提供作為應該覆寫資料分類的原因。</p></td>
<td><p>just = IW 輸入理由字串</p>
<p>只有在使用者報告覆寫時才會記錄理由欄位。</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>ruleId</p></td>
<td><p>規則的 ID</p></td>
<td><p>ruleId=GUID</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>dlpId</p></td>
<td><p>DLP 原則的 ID。 此欄位是可選的；如果沒有 dlpId，則規則不屬於 DLP 原則。</p></td>
<td><p>dlpId=GUID</p></td>
<td><p>選用</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>st</p></td>
<td><p>規則的上次修改日期</p></td>
<td><p>st=UTC 日期及時間</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>action</p></td>
<td><p>依規則採取的動作；每一個規則可具備多個動作</p></td>
<td><p>action=單一動作</p>
<p>如果一個規則有多個動作，則會有多個動作欄位。</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>sev</p></td>
<td><p>規則的稽核嚴重性</p></td>
<td><p>sev = 1、 2 或 3</p>
<p>其中 1 表示低，2 表示中，而 3 表示高。</p></td>
<td><p>選用</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>模式</p></td>
<td><p>叫用時的規則狀態 (強制執行、稽核或 auditandnotify)。</p></td>
<td><p>mode = 稽核、auditandnotify 或強制執行</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>loadW</p></td>
<td><p>載入牆上時間；該欄位是可選的</p></td>
<td><p>loadW = 時間毫秒</p></td>
<td><p>選用</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>loadC</p></td>
<td><p>載入 CPU 時間；該欄位是可選的</p></td>
<td><p>loadC = 時間毫秒</p></td>
<td><p>選用</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>execW</p></td>
<td><p>執行牆上時間；該欄位是可選的</p></td>
<td><p>execW = 時間毫秒</p></td>
<td><p>選用</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>execC</p></td>
<td><p>執行 CPU 時間；該欄位是可選的</p></td>
<td><p>execC = 時間毫秒</p></td>
<td><p>選用</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>message-id</p></td>
<td><p>郵件 ID</p></td>
<td><p>message-id = 郵件 ID</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>date-time</p></td>
<td><p>以國際標準時間傳送郵件的日期與時間</p></td>
<td><p>date-time = UTC 日期及時間</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>sender-address</p></td>
<td><p>在寄件者欄位中指定的電子郵件地址</p></td>
<td><p>sender-address = 電子郵件地址</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>recipient-address</p></td>
<td><p>郵件收件者的電子郵件地址</p></td>
<td><p>recipient-address = 電子郵件地址</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>message-subject</p></td>
<td><p>在郵件的主旨欄位中找到的資料</p></td>
<td><p>message-subject = 使用者輸入主旨字串</p></td>
<td><p>強制性</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[建立 DLP 原則偵測附隨報告](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)

[使用傳遞回報追蹤郵件](track-messages-with-delivery-reports-exchange-2013-help.md)

