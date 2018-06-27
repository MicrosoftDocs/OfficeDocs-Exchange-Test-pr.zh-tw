---
title: 'Exchange 2013 services 概觀: Exchange 2013 Help'
TOCTitle: Exchange 2013 services 概觀
ms:assetid: 2ed45d18-2ff3-4099-b841-050eb16a416b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423542(v=EXCHG.150)
ms:contentKeyID: 74479256
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 services 概觀

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-10-20_

在安裝時的Exchange Server 2013，安裝程式會執行一組新的服務安裝 Microsoft Windows中的工作。服務是伺服器的可透過Windows服務控制管理員啟動期間啟動背景處理程序。服務是設計用來操作各自與系統管理介入的可執行檔。服務可以使用圖形化使用者介面 (GUI) 模式或主控台模式來執行。

所有舊版Exchange都包含實作為服務的元件。每個Exchange伺服器角色包含服務的一部分 （或是可能所需的） 來執行其功能的伺服器角色。請注意某些服務僅成為作用儲存格時使用特定的功能。

本主題中的各節說明Exchange 2013 Mailbox server、 Client Access server 及 Edge Transport server 上所安裝的各種服務。會標示為選用的服務，您可以停用服務若您決定貴組織不需要服務所提供的功能。

## Exchange Exchange 2013 Mailbox server 上的服務

下表說明在信箱伺服器安裝Exchange服務。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>服務名稱</th>
<th>服務簡短名稱</th>
<th>描述和依存性</th>
<th>預設啟動類型</th>
<th>安全性範圍</th>
<th>相依性</th>
<th>必要或選用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>提供給Exchange服務Active Directory拓撲資訊。如果此服務已停止，大部分Exchange服務無法啟動。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Net.TCP Port Sharing Service</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 反垃圾郵件更新</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>提供Exchange SmartScreen 垃圾郵件定義更新。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 2016 年 11 月 1，Microsoft 停止產生 Exchange 和 Outlook 中 SmartScreen 篩選器的垃圾郵件定義更新。現有的 SmartScreen 垃圾郵件定義將會保留，但其效果可能會隨著時間降低。如需詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook 和 Exchange 中 SmartScreen 的取代支援</a>。</td>
</tr>
</tbody>
</table>

</td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>選用</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft ExchangeDAG 管理</p></td>
<td><p>MSExchangeDagMgmt</p></td>
<td><p>提供資料庫可用性群組 (Dag) 中的信箱伺服器的儲存區與資料庫的版面配置管理功能。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p>
<p>Net.TCP Port Sharing Service</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange診斷</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>提供監視Exchange伺服器健康情況代理程式。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>無</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange EdgeSync</p></td>
<td><p>MSExchangeEdgeSync</p></td>
<td><p>信箱伺服器與UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) 訂閱 Edge Transport server 上之間複製組態和收件者的資料安全 LDAP 通道上。</p>
<p>如果您沒有任何已訂閱的 Edge Transport server，您可以停用此服務。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>選用</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange健全狀況管理員</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>監視Exchange伺服器上的主要元件的狀況的受管理可用性的一部分。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Windows事件記錄檔</p>
<p>WindowsManagement Instrumentation</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft ExchangeIMAP4 後端</p></td>
<td><p>MSExchangeIMAP4BE</p></td>
<td><p>接收來自代理的用戶端連線從用戶端存取伺服器上的 IMAP4 服務。根據預設，不執行這項服務，所以 IMAP4 用戶端無法連線至Exchange伺服器直到此服務已啟動。</p>
<p>如果您沒有任何 IMAP4 用戶端，您可以停用此服務。</p></td>
<td><p>手動</p></td>
<td><p>網路服務</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>選用</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 資訊儲存庫</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>管理伺服器上的信箱資料庫。如果此服務已停止，就無法使用 [伺服器上的信箱資料庫。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p>
<p>遠端程序呼叫 (RPC)</p>
<p>伺服器</p>
<p>Windows事件記錄檔</p>
<p>工作站</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 信箱助理員</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>在伺服器上的信箱資料庫中執行背景處理的信箱。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange信箱複寫</p></td>
<td><p>MSExchangeMailboxReplication</p></td>
<td><p>程序的信箱移動與移動要求。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p>
<p>Net.TCP Port Sharing Service</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft ExchangeMailbox Transport 傳遞</p></td>
<td><p>MSExchangeDelivery</p></td>
<td><p>從Microsoft Exchange （本機或遠端信箱伺服器上） 的傳輸服務接收 SMTP 郵件，並將其傳遞至使用 RPC 本機信箱資料庫。</p></td>
<td><p>自動</p></td>
<td><p>網路服務</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange信箱傳輸提交</p></td>
<td><p>MSExchangeSubmission</p></td>
<td><p>從本機信箱資料庫、 接收 RPC 訊息，並透過 SMTP 提交給Microsoft Exchange （本機或遠端信箱伺服器上） 的傳輸服務。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft ExchangePOP3 後端</p></td>
<td><p>MSExchangePOP3BE</p></td>
<td><p>從用戶端存取伺服器上的 POP3 服務接收代理的用戶端連線。根據預設，不執行這項服務，所以 POP3 用戶端無法連線至Exchange伺服器直到此服務已啟動。</p></td>
<td><p>手動</p></td>
<td><p>網路服務</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>選用</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 複寫服務</p></td>
<td><p>MSExchangeRepl</p></td>
<td><p>提供在資料庫中的信箱資料庫可用性群組 (Dag) 複寫功能。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange RPC 用戶端存取</p></td>
<td><p>MSExchangeRPC</p></td>
<td><p>管理Exchange的用戶端 RPC 連線。</p></td>
<td><p>自動</p></td>
<td><p>網路服務</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange搜尋</p></td>
<td><p>MSExchangeFastSearch</p></td>
<td><p>提供信箱內容，以改善效能的內容搜尋編製索引。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange搜尋主機控制器</p></td>
<td><p>HostControllerService</p></td>
<td><p>提供部署和管理服務應用程式的本機Exchange伺服器上。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>HTTP 服務</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Server Extension for Windows Server Backup</p></td>
<td><p>WSBExchange</p></td>
<td><p>可讓Windows Server備份及還原Exchange server 資料的備份。</p></td>
<td><p>手動</p></td>
<td><p>本機系統</p></td>
<td><p>無</p></td>
<td><p>選用</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>提供服務主機Exchange元件擁有自己的服務。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 節流</p></td>
<td><p>MSExchangeThrottling</p></td>
<td><p>提供使用者工作負載管理限制 （前身為使用者節流） 的使用者作業的速率。</p></td>
<td><p>自動</p></td>
<td><p>網路服務</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 傳輸</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>提供的 SMTP 伺服器和傳輸堆疊。</p></td>
<td><p>自動</p></td>
<td><p>網路服務</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p>
<p>Microsoft篩選管理服務</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 傳輸記錄搜尋</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>提供遠端搜尋功能，以傳輸記錄檔 （例如郵件追蹤）。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>選用</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 整合通訊</p></td>
<td><p>MSExchangeUM</p></td>
<td><p>提供整合通訊 (UM) 功能： 可讓語音和傳真訊息儲存在Exchange及提供的使用者電話存取電子郵件、 語音信箱、 行事曆、 連絡人或自動語音應答。如果此服務已停止，無法使用整合通訊。</p>
<p>如果您未使用 UM，您可以停用此服務。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>CNG 主要隔離</p>
<p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>選用</p></td>
</tr>
</tbody>
</table>


## Exchange Exchange 2013 Client Access server 上的服務

下表說明用戶端存取伺服器安裝Exchange服務。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>服務名稱</th>
<th>服務簡短名稱</th>
<th>描述和依存性</th>
<th>預設啟動類型</th>
<th>安全性範圍</th>
<th>相依性</th>
<th>必要或選用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>提供給Exchange服務Active Directory拓撲資訊。如果此服務已停止，大部分Exchange服務無法啟動。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Net.TCP Port Sharing Service</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange診斷</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>提供監視Exchange伺服器健康情況代理程式。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>無</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft ExchangeFrontend 傳輸</p></td>
<td><p>MSExchangeFrontEndTransport</p></td>
<td><p>以Microsoft Exchange Mailbox server 上的傳輸服務的外部主機分開的 proxy SMTP 連線。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange健全狀況管理員</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>監視Exchange伺服器上的主要元件的狀況的受管理可用性的一部分。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Windows事件記錄檔</p>
<p>WindowsManagement Instrumentation</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4</p></td>
<td><p>MSExchangeIMAP4</p></td>
<td><p>Proxy IMAP4 IMAP4 服務 Mailbox server 上的用戶端連線。根據預設，不執行這項服務，所以 IMAP4 用戶端無法連線至Exchange伺服器直到此服務已啟動。</p>
<p>如果您沒有任何 IMAP4 用戶端，您可以停用此服務。</p></td>
<td><p>手動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>選用</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange POP3</p></td>
<td><p>MSExchangePOP3</p></td>
<td><p>Proxy POP3 信箱伺服器上的 IMAP4 服務的用戶端連線。根據預設，不執行這項服務，所以 POP3 用戶端無法連線至Exchange伺服器直到此服務已啟動。</p></td>
<td><p>手動</p></td>
<td><p>網路服務</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>選用</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange搜尋主機控制器</p></td>
<td><p>HostControllerService</p></td>
<td><p>提供部署和管理服務應用程式的本機Exchange伺服器上。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>HTTP 服務</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>提供服務主機Exchange元件擁有自己的服務。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange整合通訊呼叫路由器</p></td>
<td><p>MSExchangeUMCR</p></td>
<td><p>將 UM 用戶端連線重新導向至在信箱伺服器上的 Unified Messaging 服務。</p>
<p>如果您未使用 UM，您可以停用此服務。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>CNG 主要隔離</p>
<p>Microsoft Exchange Active Directory 拓撲</p></td>
<td><p>選用</p></td>
</tr>
</tbody>
</table>


## Exchange Exchange 2013 Edge Transport server 上的服務

下表說明安裝在 Edge Transport server 的Exchange服務。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>服務名稱</th>
<th>服務簡短名稱</th>
<th>描述</th>
<th>預設啟動類型</th>
<th>安全性範圍</th>
<th>相依性</th>
<th>必要或選用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>ADAM_MSExchange</p></td>
<td><p>Edge Transport server 上儲存組態資料和收件者的資料。這項服務代表UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) Exchange安裝程式會自動建立的具名執行個體。</p></td>
<td><p>自動</p></td>
<td><p>網路服務</p></td>
<td><p>COM + 事件系統</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 反垃圾郵件更新</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>提供Exchange SmartScreen 垃圾郵件定義更新。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 2016 年 11 月 1，Microsoft 停止產生 Exchange 和 Outlook 中 SmartScreen 篩選器的垃圾郵件定義更新。現有的 SmartScreen 垃圾郵件定義將會保留，但其效果可能會隨著時間降低。如需詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook 和 Exchange 中 SmartScreen 的取代支援</a>。</td>
</tr>
</tbody>
</table>

</td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>選用</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 認證服務</p></td>
<td><p>MSExchangeEdgeCredential</p></td>
<td><p>監視UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) 中的認證變更並安裝在 Edge Transport server 上所做的變更。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange診斷</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>提供監視Exchange伺服器健康情況代理程式。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>無</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange健全狀況管理員</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>監視Exchange伺服器上的主要元件的狀況的受管理可用性的一部分。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Windows 事件記錄檔</p>
<p>Windows Management Instrumentation</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>提供服務主機Exchange元件擁有自己的服務。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>必要</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 傳輸</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>提供的 SMTP 伺服器和傳輸堆疊。</p></td>
<td><p>自動</p></td>
<td><p>網路服務</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>必要</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 傳輸記錄搜尋</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>提供遠端搜尋功能，以傳輸記錄檔 （例如郵件追蹤）。</p></td>
<td><p>自動</p></td>
<td><p>本機系統</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>選用</p></td>
</tr>
</tbody>
</table>

