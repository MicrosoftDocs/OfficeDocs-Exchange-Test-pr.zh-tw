---
title: 'Exchange 2013 中用戶端和郵件流程的網路連接埠: Exchange 2013 Help'
TOCTitle: Exchange 2013 中用戶端和郵件流程的網路連接埠
ms:assetid: fec09455-e99e-42eb-8b32-1ddc08d9a19e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb331973(v=EXCHG.150)
ms:contentKeyID: 64131353
ms.date: 01/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中用戶端和郵件流程的網路連接埠

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題提供 MicrosoftExchange Server 2013 與電子郵件用戶端、網際網路郵件伺服器和本機 Exchange 組織外部的其他服務進行通訊所使用的網路連接埠的相關資訊。在我們進入該內容之前，先了解下列的基本規則：

  - 我們不支援在任何或所有類型拓撲中限制或改變內部 Exchange 伺服器之間、內部 Exchange 伺服器和內部 Lync 或 商務用 Skype 伺服器之間，或內部 Exchange 伺服器和內部 Active Directory 網域控制站之間的網路流量。如果您有可能會限制或變更這類網路流量的防火牆或網路裝置，您需要設定可允許在這些伺服器之間自由且不受限制通訊的規則 (允許任何連接埠上的傳入和傳出網路流量的規則 — 包括隨機 RPC 連接埠 — 以及絕不會在網路上更改位元的任何通訊協定)。

  - Edge Transport Server 幾乎都在周邊網路中，因此預期您將限制 Edge Transport Server 與網際網路之間，以及 Edge Transport Server 與您的內部 Exchange 組織之間的網路流量。本主題將說明這些網路連接埠。

  - 預期您將限制外部用戶端和服務與您的內部 Exchange 組織之間的網路流量。如果您決定要限制內部用戶端之間與內部 Exchange 伺服器之間的網路流量也可以。本主題將說明這些網路連接埠。

**目錄**

用戶端和服務所需的網路連接埠

郵件流程所需的網路連接埠 (沒有 Edge Transport Server)

Edge Transport Server 的郵件流程所需的網路連接埠

混合部署所需的網路連接埠

整合通訊所需的網路連接埠

## 用戶端和服務所需的網路連接埠

電子郵件用戶端存取 Exchange 組織中的信箱及其他服務所需的網路連接埠如下圖表所述。

**附註：**

  - 這些用戶端和服務的目的地是 Client Access Server。這可以是獨立的 Client Access Server，或是一部 Client Access Server 與 Mailbox Server 安裝在相同電腦上。

  - 雖然圖表顯示來自網際網路的用戶端和服務，概念也適用內部用戶端 (例如，在資源樹系中存取 Exchange 伺服器的帳戶樹系中的用戶端)。同樣地，表格沒有來源欄，是因為來源可以是 Exchange 組織外部的任何位置 (例如，網際網路或帳戶樹系)。

  - Edge Transport Server 沒有參與在與這些用戶端和服務相關的網路流量。

![用戶端和服務所需的網路連接埠](images/Bb331973.f5ba3439-f001-43c8-848e-0e3fd0fce931(EXCHG.150).png "用戶端和服務所需的網路連接埠")


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>用途</th>
<th>連接埠</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>下列用戶端和服務使用的加密網頁連結：</p>
<ul>
<li><p>自動探索服務</p></li>
<li><p>Exchange ActiveSync</p></li>
<li><p>Exchange Web 服務 (EWS)</p></li>
<li><p>離線通訊錄發佈</p></li>
<li><p>Outlook 無所不在 (RPC over HTTP)</p></li>
<li><p>Outlook MAPI over HTTP</p></li>
<li><p>Outlook Web App</p></li>
</ul></td>
<td><p>443/TCP (HTTPS)</p></td>
<td><p>如需這些用戶端和服務的相關資訊，請參閱下列主題：</p>
<ul>
<li><p><a href="autodiscover-service-for-exchange-2013.md">自動探索服務</a></p></li>
<li><p><a href="exchange-activesync-exchange-2013-help.md">Exchange ActiveSync</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/?linkid=529544">Exchange 的 EWS 參考</a></p></li>
<li><p><a href="offline-address-books-exchange-2013-help.md">離線通訊錄</a></p></li>
<li><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook 無所不在</a></p></li>
<li><p><a href="mapi-over-http-exchange-2013-help.md">MAPI over HTTP</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中 Outlook Web App 的新功能</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>下列用戶端和服務使用的未加密網頁連結：</p>
<ul>
<li><p>網際網路行事曆發佈</p></li>
<li><p>Outlook Web App (重新導向至 443/TCP)</p></li>
<li><p>自動探索 (443/TCP 無法使用時後援)</p></li>
</ul></td>
<td><p>80/TCP (HTTP)</p></td>
<td><p>可能的話，我們建議在 443/TCP 使用加密的網頁連線，來協助保護資料和認證。不過，您可能會發現，必須將有些服務設定為在 80/TCP 上使用未加密的網路連線連至 Client Access Server。</p>
<p>如需這些用戶端和服務的相關資訊，請參閱下列主題：</p>
<ul>
<li><p><a href="enable-internet-calendar-publishing-exchange-2013-help.md">啟用網際網路行事曆發佈</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中 Outlook Web App 的新功能</a></p></li>
<li><p><a href="autodiscover-service-for-exchange-2013.md">自動探索服務</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>IMAP4 用戶端</p></td>
<td><p>143/TCP (IMAP)，993/TCP (安全 IMAP)</p></td>
<td><p>預設會停用 IMAP4。如需詳細資訊，請參閱 <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">Exchange Server 2013 中的 POP3 和 IMAP4</a>。</p>
<p>Client Access Server 上的 IMAP4 服務代理連線至 Mailbox Server 上的 IMAP4 後端服務。</p></td>
</tr>
<tr class="even">
<td><p>POP3 用戶端</p></td>
<td><p>110/TCP (POP3)，995/TCP (安全 POP3)</p></td>
<td><p>預設會停用 POP3。如需詳細資訊，請參閱 <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">Exchange Server 2013 中的 POP3 和 IMAP4</a>。</p>
<p>Client Access Server 上的 POP3 服務代理連線至 Mailbox Server 上的 POP3 後端服務。</p></td>
</tr>
<tr class="odd">
<td><p>SMTP 用戶端 (已驗證)</p></td>
<td><p>587/TCP (已驗證的 SMTP)</p></td>
<td><p>Client Access Server 上名為「用戶端前端 <em>&lt;Server name&gt;</em>」的預設接收連接器會連接埠 587 上接聽已驗證的 SMTP 用戶端傳送。</p>
<p><strong>附註：</strong></p>
<p>如果您的郵件用戶端只能在連接埠 25 上提交驗證的 SMTP 郵件，您可以修改此接收連接器的網路介面卡繫結值，也可以同時接聽連接埠 25 上已驗證的 SMTP 郵件提交。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 郵件流程所需的網路連接埠

在您的 Exchange 組織之間往返傳送郵件的方式取決於您的 Exchange 拓撲。最重要的因素是您是否在周邊網路中具備部署的已訂閱 Edge Transport Server。

## 郵件流程所需的網路連接埠 (沒有 Edge Transport Server)

下表說明在僅 Client Access Server 和 Mailbox Server 的 Exchange 組織中郵件流程所需的網路連接埠。下圖顯示不同的 Mailbox 和 Client Access Server，不論 Client Access Server 和 Mailbox Server 是否安裝在相同電腦或不同電腦上，概念都是相同的。

![郵件流程所需的網路連接埠 (沒有 Edge Transport Server)](images/Bb331973.af54dfd3-fe6b-4b6e-bb8e-b00df94a0be0(EXCHG.150).png "郵件流程所需的網路連接埠 (沒有 Edge Transport Server)")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>用途</th>
<th>連接埠</th>
<th>來源</th>
<th>Destination</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>輸入郵件</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>網際網路 (任何)</p></td>
<td><p>Client Access server</p></td>
<td><p>Client Access Server 上名為「預設前端 <em>&lt;Client Access server name&gt;</em>」的預設接收連接器會在連接埠 25 上接聽匿名的輸入 SMTP 郵件。</p>
<p>郵件會使用隱含和不可見的內部組織傳送連接器從 Client Access Server 轉送到 Mailbox Server，該連接器能在相同組織中 Exchange 伺服器之間自動路由傳送郵件。</p></td>
</tr>
<tr class="even">
<td><p>輸出郵件</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>信箱伺服器</p></td>
<td><p>網際網路 (任何)</p></td>
<td><p>根據預設，Exchange 不會建立可讓您將郵件傳送至網際網路的任何傳送連接器。您必須手動建立傳送連接器。如需詳細資訊，請參閱<a href="send-connectors-exchange-2013-help.md">傳送連接器</a>。</p></td>
</tr>
<tr class="odd">
<td><p>輸出郵件 (如果透過 Client Access Server 路由傳送)</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Client Access server</p></td>
<td><p>網際網路 (任何)</p></td>
<td><p>傳送連接器在只有 Exchange 系統管理中心中設定了<strong>透過 Client Access Server 代理</strong>或 <code>-FrontEndProxyEnabled $true</code> (Exchange 管理命令介面 中) 時，才能透過 Client Access Server 路由傳送輸出郵件。</p>
<p>在此情況下，Client Access Server 上名為「輸出 Proxy 前端 <em>&lt;Client Access server name&gt;</em>」的預設接收連接器會接聽來自 Mailbox Server 的輸出郵件。如需詳細資訊，請參閱<a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">建立電子郵件傳送至網際網路的傳送連接器</a>。</p></td>
</tr>
<tr class="even">
<td><p>下一個郵件躍點的名稱解析的 DNS (未附圖)</p></td>
<td><p>53/UDP，53/TCP (DNS)</p></td>
<td><p>面向網際網路的 Exchange 伺服器 (Client Access Server 或 Mailbox Server)</p></td>
<td><p>DNS 伺服器</p></td>
<td><p>請參閱名稱解析一節。</p></td>
</tr>
</tbody>
</table>


回到頁首

## Edge Transport Server 的郵件流程所需的網路連接埠

安裝在周邊網路中訂閱的 Edge Transport Server 基本上可消除透過 Client Access Server 的 SMTP 郵件流程。特別是：

  - 來自 Exchange 組織的輸出郵件永遠不會經由 Client Access Server。郵件一律會流經訂閱的 Active Directory 網站中的 Mailbox Server 至 Edge Transport Server (而不論 Edge Transport Server 上的 Exchange 版本為何)。

  - 輸入郵件永遠不會經由獨立 Client Access Server。郵件從 Edge Transport Server 流往訂閱的 Active Directory 站台中的 Mailbox Server。如果 Mailbox Server 和 Client Access Server 安裝在相同電腦上，來自 Exchange 2013 Edge Transport Server 的郵件會先到達前端傳輸服務電腦 (Client Access Server 角色)，之後才流向傳輸服務 (Mailbox Server 角色)。Exchange 2007 或 Exchange 2010 Edge Transport Server 一律會直接將郵件傳送到傳輸服務，即使 Mailbox Server 及 Client Access Server 安裝在相同電腦上。

如需詳細資訊，請參閱[郵件流程](mail-flow-exchange-2013-help.md)。

下表說明具有 Edge Transport Server 的 Exchange 組織中郵件流程所需的網路連接埠。除非另有說明，不論 Client Access Server 和 Mailbox Server 是否安裝在相同電腦或不同電腦上，概念都是相同的。

![Edge Transport Server 的郵件流程所需的網路連接埠](images/Bb331973.110c79b3-dbd9-4cb5-bba1-02048363ee1c(EXCHG.150).png "Edge Transport Server 的郵件流程所需的網路連接埠")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>用途</th>
<th>連接埠</th>
<th>來源</th>
<th>Destination</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>輸入郵件 - 網際網路至 Edge Transport Server</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>網際網路 (任何)</p></td>
<td><p>Edge Transport server</p></td>
<td><p>Edge Transport Server 上名為「預設內部接收連接器 <em>&lt;Edge Transport server name&gt;</em>」的預設接收連接器會在連接埠 25 上接聽匿名 SMTP 郵件。</p></td>
</tr>
<tr class="even">
<td><p>輸入郵件 - Edge Transport Server 至內部 Exchange 組織</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Edge Transport server</p></td>
<td><p>訂閱的 Active Directory 站台中的信箱伺服器</p></td>
<td><p>名為「EdgeSync - 輸入至 <em>&lt;Active Directory site name&gt;</em>」的預設傳送連接器會在連接埠 25 上將輸入郵件轉送至訂閱的 Active Directory 站台中的任何 Mailbox Server。如需詳細資訊，請參閱<a href="edge-subscriptions-exchange-2013-help.md">Edge 訂閱</a>主題中的「傳送在 Edge 訂閱程序期間建立的連接器」一節。</p>
<p>實際接收郵件的服務取決於 Mailbox Server 和 Client Access Server 是安裝在相同電腦或不同電腦上。</p>
<ul>
<li><p><strong>獨立 Mailbox Server</strong>   名為「預設 <em>&lt;Mailbox server name&gt;</em>」的預設接收連接器會在連接埠 25 接聽輸入郵件 (包括來自 Edge Transport Server 的郵件)。</p></li>
<li><p><strong>Mailbox Server 和 Client Access Server 安裝在相同電腦上</strong>   前端傳輸服務 (Client Access Server 角色) 中名為「預設前端 <em>&lt;Server name&gt;</em>」的預設接收連接器會在連接埠 25 上接聽傳入郵件 (包括來自 Exchange 2013 Edge Transport Server 的郵件)。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>輸出郵件 - 內部 Exchange 組織到 Edge Transport Server</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>訂閱的 Active Directory 站台中的信箱伺服器</p></td>
<td><p>Edge Transport Server</p></td>
<td><p>輸出郵件永遠會略過 Client Access Server。</p>
<p>郵件會使用隱含和不可見的內部組織傳送連接器從訂閱的 Active Directory 網站中的任何 Mailbox Server 轉送到 Edge Transport Server，該連接器能在相同組織中的 Exchange 伺服器之間自動路由傳送郵件。</p>
<p>Edge Transport Server 上名為「預設內部接收連接器 <em>&lt;Edge Transport server name&gt;</em>」的預設接收連接器，會在連接埠 25 上接聽來自訂閱的 Active Directory 站台中任何 Mailbox Server 的 SMTP 郵件 。</p></td>
</tr>
<tr class="even">
<td><p>輸出郵件 - Edge Transport Server 至網際網路</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Edge Transport server</p></td>
<td><p>網際網路 (任何)</p></td>
<td><p>預設的傳送連接器名稱為「EdgeSync - <em>&lt;Active Directory site name&gt;</em> 至網際網路」，在連接埠 25 上轉送輸出郵件從 Edge Transport Server至網際網路。</p></td>
</tr>
<tr class="odd">
<td><p>EdgeSync 同步處理</p></td>
<td><p>50636/TCP (安全 LDAP)</p></td>
<td><p>參與 EdgeSync 同步處理的訂閱的 Active Directory 站台中的信箱伺服器</p></td>
<td><p>Edge Transport Server</p></td>
<td><p>當 Edge Transport Server 訂閱 Active Directory 站台，當時存在於網站的所有 Mailbox Server 都會參與 EdgeSync 同步處理。不過，您稍後新增的任何 Mailbox Server 不會自動參與 EdgeSync 同步處理。</p></td>
</tr>
<tr class="even">
<td><p>下一個郵件躍點的名稱解析的 DNS (未附圖)</p></td>
<td><p>53/UDP，53/TCP (DNS)</p></td>
<td><p>Edge Transport server</p></td>
<td><p>DNS 伺服器</p></td>
<td><p>請參閱名稱解析一節。</p></td>
</tr>
<tr class="odd">
<td><p>寄件者信譽的 Proxy 伺服器定義 (未附圖)</p></td>
<td><p>使用者定義</p></td>
<td><p>Edge Transport Server</p></td>
<td><p>網際網路</p></td>
<td><p>寄件者信譽 (通訊協定分析代理程式) 會分析輸入郵件路徑，以減少垃圾郵件。如果您的組織使用 Proxy 伺服器來控制對網際網路的存取，您需要定義 Proxy 伺服器的詳細資料，使寄件者信譽可以正常運作 (特別是開放 Proxy 偵測和寄件者封鎖)。您使用 <strong>Set-SenderReputationConfig</strong> Cmdlet 上的 <em>ProxyServerName</em>、<em>ProxyServerPort</em> 和 <em>ProxyServerType</em> 參數來定義您的組織 Proxy 伺服器，讓寄件者信譽可以成功連線至網際網路。如需詳細資訊，請參閱<a href="manage-sender-reputation-exchange-2013-help.md">管理寄件者信譽</a>。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 名稱解析

下一個郵件躍點的 DNS 解析是任何 Exchange 組織中郵件流程的基礎。負責接收輸入郵件的 Exchange 伺服器，或傳送輸出郵件的伺服器，都必須能夠解析內部和外部的主機名稱，才能適當路由傳送郵件。而所有內部 Exchange 伺服器必須能夠解析內部主機名稱，才能執行適當的郵件路由。有許多不同的方式可設計 DNS 基礎結構，但重要的結果就是確保下一個躍點的名稱解析能對您所有的 Exchange 伺服器正常運作。

## 混合部署需要的網路連接埠

同時使用 Exchange 2013 和 MicrosoftOffice 365 的組織所需的網路連接埠會在[混合部署必要條件](https://technet.microsoft.com/zh-tw/library/hh534377\(v=exchg.150\))的「混合式部署通訊協定、連接埠和端點」一節中說明。

## 整合通訊所需的網路連接埠

下列主題涵蓋整合通訊所需的網路連接埠：

  - [UM 通訊協定、 連接埠和服務](um-protocols-ports-and-services-exchange-2013-help.md)

  - [Exchange Server 2013 SP1 架構海報](https://go.microsoft.com/fwlink/p/?linkid=518646)

回到頁首

