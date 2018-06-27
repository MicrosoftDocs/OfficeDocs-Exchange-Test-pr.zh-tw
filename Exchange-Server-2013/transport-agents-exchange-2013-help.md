---
title: '傳輸代理程式: Exchange 2013 Help'
TOCTitle: 傳輸代理程式
ms:assetid: e7389d63-3172-40d5-bf53-0d7cd7e78340
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125012(v=EXCHG.150)
ms:contentKeyID: 50474485
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳輸代理程式

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

傳輸代理程式可讓您安裝 Microsoft、 協力廠商或組織的 Exchange 伺服器上建立的自訂軟體。此軟體可然後處理通過傳輸管線的電子郵件。在 Microsoft Exchange Server 2013、 傳輸管線是進行下列程序：

  - Client Access server 上 Front End Transport 服務

  - 在信箱伺服器上傳輸服務

  - 在 Mailbox server 上 Mailbox Transport service

  - 在 Edge Transport server 的傳輸服務

如需傳輸管線的詳細資訊，請參閱[郵件流程](mail-flow-exchange-2013-help.md)

Exchange 舊版、 like Exchange 2013傳輸提供透過 Microsoft Exchange Server 2013傳輸代理程式 SDK 的擴充性。SDK Exchange 2013版本根據Microsoft.NET Framework 4.0 版，並允許實作下列預先定義的類別的協力廠商提供：

  - **SmtpReceiveAgent**

  - **RoutingAgent**

  - **DeliveryAgent**

當符合針對 SDK 中的文件庫，所產生的組件並登錄Exchange 2013，以載入代理程式以及特定的 SMTP 工作階段或郵件處理階段期間，叫用其事件處理常式。下列階段或事件屬於代理程式定義。代理程式登錄資訊會儲存在 XML 組態檔。

下列清單說明使用Exchange 2013中的傳輸代理程式的需求。

  - Mailbox server 及 Edge Transport server 上的傳輸服務完全支援預先定義的所有類別的 SDK、 與因此任何協力廠商傳輸代理程式撰寫集線傳輸或 Edge Transport server 中 Microsoft Exchange Server 2010角色應該在Exchange 2013中的傳輸服務中運作。

  - Front End Transport 服務僅支援**SmtpReceiveAgent**類別的 SDK 及第三方代理程式無法操作**OnEndOfData** SMTP 事件。

  - 信箱傳輸服務不支援 SDK，因此您無法使用任何協力廠商代理程式的信箱傳輸服務中。

支援的舊版傳輸代理程式根據.NET Framework 4.0 版之前的版本不預設啟用，但您可以啟用它。指示，請參閱[啟用支援的舊版傳輸代理程式](enable-support-for-legacy-transport-agents-exchange-2013-help.md)。

**目錄**

傳輸代理程式管理的更新

傳輸代理程式及 SMTP 事件

傳輸代理程式的優先順序

內建傳輸代理程式

疑難排解傳輸代理程式

## 傳輸代理程式管理的更新

由於Exchange 2013傳輸管線的更新，而傳輸代理程式指令程式需要區分的傳輸服務及 Front End Transport 服務，尤其是在同一部電腦上已安裝 Client Access server 和 Mailbox server。如需詳細資訊，請參閱[管理傳輸代理程式](manage-transport-agents-exchange-2013-help.md)。

傳輸代理程式管理指令程式來管理設定檔位於`%ExchangeInstallPath%TransportRoles\Shared`。Mailbox server 及 Edge Transport server 上的傳輸服務，該檔案是`agents.config`。Client Access server 上 Front End Transport 服務檔案是`fetagents.config`。這兩個檔案使用相同Exchange 2010不同的格式。如需管理傳輸代理程式的詳細資訊，請參閱[管理傳輸代理程式](manage-transport-agents-exchange-2013-help.md)。

回到頁首

## 傳輸代理程式及 SMTP 事件

傳輸代理程式使用 SMTP 事件。郵件進入傳輸管線會觸發這些事件。SMTP 事件讓傳輸代理程式存取郵件於特定時間點 SMTP 交談期間及期間的郵件通過組織路由。

請注意Exchange 2013中有新的 SMTP 接收事件。SMTP 接收存在於用戶端存取伺服器、 信箱伺服器與 Edge Transport server 上的傳輸服務及 Mailbox server 上的 Mailbox Transport 傳遞服務上 Front End Transport 服務。分類程式只存在於信箱伺服器與 Edge Transport server 上的傳輸服務。如需傳輸服務與分類程式的詳細資訊，請參閱[郵件路由](mail-routing-exchange-2013-help.md)。

下表列出提供存取傳輸管線中的郵件的 SMTP 事件。

### SMTP 接收事件

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>順序</th>
<th>SMTP 事件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong></p></td>
<td><p>從遠端 SMTP 主機的初始連線來觸發這個事件。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnHeloCommand</strong></p></td>
<td><p>此事件觸發時<code>HELO</code>命令遠端 SMTP 主機所發出。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnEhloCommand</strong></p></td>
<td><p>此事件觸發時<code>EHLO</code>命令遠端 SMTP 主機所發出。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnStartTlsCommand</strong></p></td>
<td><p>此事件觸發時<code>STARTTLS</code>命令遠端 SMTP 主機所發出。</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p><strong>OnAuthCommand</strong></p></td>
<td><p>此事件觸發時<code>AUTH</code>命令遠端 SMTP 主機所發出。</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p><strong>OnProcessAuthentication</strong></p></td>
<td><p>當正在處理與遠端 SMTP 主機驗證觸發此事件。</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p><strong>OnEndOfAuthentication</strong></p></td>
<td><p>遠端 SMTP 主機完成之後驗證觸發此事件。</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p><strong>OnXSessionParamsCommand</strong></p></td>
<td><p>此事件觸發時<code>XSESSIONPARAMS</code>命令遠端 SMTP 主機所發出。</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>此事件觸發時<code>MAIL FROM</code>命令遠端 SMTP 主機所發出。</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p><strong>OnRcptToCommand</strong></p></td>
<td><p>此事件觸發時<code>RCPT TO</code>命令遠端 SMTP 主機所發出。</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p><strong>OnDataCommand</strong></p></td>
<td><p>遠端 SMTP 主機所發出的<code>DATA</code> （文字） 或<code>BDAT</code> （二進位資料） 命令時就會觸發此事件。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>遠端 SMTP 主機完成送出的電子郵件訊息標頭時就會觸發此事件。這被以空白 (<code>&lt;CRLF&gt;</code>) 分隔線郵件標頭和郵件內文。</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p><strong>OnProxyInboundMessage</strong></p></td>
<td><p>此事件會觸發轉送輸入的 SMTP 工作階段時或<em>代理</em>在信箱伺服器上的傳輸服務的 Client Access server 上 Front End Transport 服務。</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>遠端 SMTP 主機問題資料命令的結束時就會觸發此事件。文字由<code>DATA</code>命令啟動工作階段，結尾的資料指標是<code>&lt;CRLF&gt;.&lt;CRLF&gt;</code>。二進位<code>BDAT</code>命令所啟動的工作階段，結尾的資料指標是<code>BDAT LAST</code>。</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnHelpCommand</strong></p></td>
<td><p>此事件會觸發<code>HELP</code>命令發出遠端 SMTP 主機。</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnNoopCommand</strong></p></td>
<td><p>此事件會觸發<code>NOOP</code>命令發出遠端 SMTP 主機。</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnReject</strong></p></td>
<td><p>如果接收 SMTP 主機對傳送 SMTP 主機發出暫時性或永久性的傳遞狀態通知 (DSN) 程式碼就會觸發此事件。</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnRsetCommand</strong></p></td>
<td><p>如果傳送的 SMTP 主機發出<code>RSET</code>命令，觸發此事件。</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p><strong>OnDisconnectEvent</strong></p></td>
<td><p>SMTP 交談所接收或傳送 SMTP 主機的中斷連線來觸發這個事件。通常，這種情況時<code>QUIT</code>命令遠端 SMTP 主機所發出。</p></td>
</tr>
</tbody>
</table>


\* \* 這些事件可能會發生在任何時候， **OnConnectEvent**之後才**OnDisconnectEvent**。

### 分類程式事件

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>順序</th>
<th>分類程式事件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
<td><p>當郵件送達時接收的 Mailbox server 或 Edge Transport server 上的傳輸服務中提交佇列中觸發此事件。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
<td><p>之後，所有收件者都已解決，但前下一步] 一個躍點已決定每個收件者會觸發這個事件。<strong>OnResolvedMessage</strong>路由事件讓後續事件來使用每個收件者<strong>SetRoutingOverride</strong>方法會覆寫預設的路由行為。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
<td><p>郵件已分類、 已展開通訊群組清單，並與收件者都已解決之後觸發此事件。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
<td><p>完成分類程式處理郵件觸發此事件。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 傳輸代理程式的優先順序

有兩個因素可判斷傳輸管線中的郵件傳輸代理程式處理的順序：

1.  其中已註冊傳輸代理程式、 SMTP 事件及該 SMTP 事件時遇到的郵件。

2.  如果有多個專員指派給傳輸代理程式的優先順序值登錄至相同的 SMTP 事件。最高的優先順序為 1。較高的整數值表示較低的代理程式優先順序。

例如，假設您已設定下列傳輸代理程式：

  - 傳輸代理程式的優先順序為 1 和優先順序為 2 的傳輸代理程式 C 被註冊於**OnEndOfHeaders** SMTP 事件。

  - 傳輸代理程式 B 優先順序為 4 被註冊於**OnMailCommand** SMTP 事件。

傳輸代理程式 B 會套用至郵件先因為**OnMailCommand**事件遇到郵件**OnEndOfHeaders**事件之前。當郵件抵達**OnEndOfHeaders**事件時，傳輸代理程式的就會套用之前傳輸代理程式 C 因為傳輸代理程式的較高的優先順序 （較低的整數值） 比傳輸代理程式 c。

## 內建傳輸代理程式

Exchange 2013包含許多內建的傳輸代理程式所提供的功能，例如反垃圾郵件、 傳輸規則和日誌記錄。充分運用Exchange 2013信箱伺服器與用戶端存取伺服器上的內建傳輸代理程式且不可見無法傳輸代理程式管理指令程式來管理。幾乎所有的檢視及可管理的內建傳輸代理程式會在 Mailbox server 及 Edge Transport server 上的傳輸服務中。

下表說明在信箱伺服器上更有趣的內建的傳輸代理程式。請注意此表格不包含許多看不見並無法管理傳輸代理程式。

### 在信箱伺服器上有趣的內建的傳輸代理程式

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>代理程式名稱</th>
<th>可管理？</th>
<th>優先順序</th>
<th>SMTP 或分類程式事件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>傳輸規則代理程式</p></td>
<td><p>是</p></td>
<td><p>1</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>惡意程式碼代理程式</p></td>
<td><p>是</p></td>
<td><p>2</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>文字郵件路由代理程式</p></td>
<td><p>是</p></td>
<td><p>3</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>文字訊息的傳遞代理程式</p></td>
<td><p>是</p></td>
<td><p>4</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>日誌代理程式</p></td>
<td><p>否</p></td>
<td><p>沒有可設定</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>日誌報告解密代理程式</p></td>
<td><p>否</p></td>
<td><p>沒有可設定</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>RMS 解密代理程式</p></td>
<td><p>否</p></td>
<td><p>沒有可設定</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>RMS 加密代理程式</p></td>
<td><p>否</p></td>
<td><p>沒有可設定</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>RMS 通訊協定解密代理程式</p></td>
<td><p>否</p></td>
<td><p>沒有可設定</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
</tbody>
</table>


Edge Transport server 上大部分的內建的傳輸代理程式會為可見及可管理傳輸代理程式管理指令程式，或其他特定功能指令程式。

下表說明更有趣但 Edge Transport server 上的內建傳輸代理程式。請注意此表不含看不見或無法管理傳輸代理程式。

### Edge Transport server 上有趣的內建的傳輸代理程式

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>代理程式名稱</th>
<th>可管理？</th>
<th>優先順序</th>
<th>SMTP 或分類程式事件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>連線篩選代理程式</p></td>
<td><p>是</p></td>
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnMailCommand</strong>, <strong>OnRcptComand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>地址修正輸入代理程式</p></td>
<td><p>是</p></td>
<td><p>2</p></td>
<td><p><strong>OnRcptCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>Edge 規則代理程式</p></td>
<td><p>是</p></td>
<td><p>3</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>內容篩選器代理程式 *</p></td>
<td><p>是</p></td>
<td><p>4</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="odd">
<td><p>寄件者識別碼代理程式 *</p></td>
<td><p>是</p></td>
<td><p>5</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>寄件者篩選器代理程式 *</p></td>
<td><p>是</p></td>
<td><p>6</p></td>
<td><p><strong>OnMailCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>收件者篩選器代理程式</p></td>
<td><p>是</p></td>
<td><p>7</p></td>
<td><p><strong>OnRcptCommand</strong></p></td>
</tr>
<tr class="even">
<td><p>通訊協定分析代理程式 *</p></td>
<td><p>是</p></td>
<td><p>8</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnEndOfHeaders</strong>, <strong>OnEndOfData</strong>, <strong>OnReject</strong>, <strong>OnRsetCommand</strong>, <strong>OnDisconnectEvent</strong></p></td>
</tr>
<tr class="odd">
<td><p>附件篩選代理程式</p></td>
<td><p>是</p></td>
<td><p>9</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>地址修正輸出代理程式</p></td>
<td><p>是</p></td>
<td><p>10</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
</tbody>
</table>


\* 您也可以安裝及設定 Mailbox server 上的這些反垃圾郵件代理程式。如需詳細資訊，請參閱[啟用信箱伺服器上的反垃圾郵件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

回到頁首

## 疑難排解傳輸代理程式

為了協助您疑難排解傳輸代理程式的問題，您可以使用下列功能：

  - **Get-transportpipeline**  此指令程式會顯示 SMTP 事件及相對應的傳輸代理程式遇到 Exchange 伺服器上的郵件。如需詳細資訊，請參閱[傳輸管線中檢視傳輸代理程式](view-transport-agents-in-the-transport-pipeline-exchange-2013-help.md)。

  - **管線追蹤**  管線追蹤會建立一則訊息之前和之後遇到每個傳輸代理程式完全快照。這可讓您尋找傳輸代理程式會導致無法預期的結果。如需詳細資訊，請參閱[管線追蹤](pipeline-tracing-exchange-2013-help.md)。

回到頁首

