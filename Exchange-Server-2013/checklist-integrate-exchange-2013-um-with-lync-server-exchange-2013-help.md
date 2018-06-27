---
title: '檢查清單： Lync Server 整合 Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 檢查清單： Lync Server 整合 Exchange 2013 UM
ms:assetid: 3b82e86f-9f30-4445-96ad-744082abeaeb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638120(v=EXCHG.150)
ms:contentKeyID: 52062535
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢查清單： Lync Server 整合 Exchange 2013 UM

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

安裝及部署整合通訊 (UM) 及Microsoft Lync Server 2013 中使用此檢查清單。本主題中 「 Lync Server 」 也參照至 Lync Server 2010。不過，Microsoft Office Communications Server 2007 R2 也可以部署與整合通訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td> </td>
</tr>
</tbody>
</table>


您開始使用這份檢查清單之前，請確定您已熟悉下列概念：

  - [部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [與 Office Communications Server 2007 R2 和 Lync Server 共存](coexistence-with-office-communications-server-2007-r2-and-lync-server-exchange-2013-help.md)

如需如何執行 Lync Server 必須完成工作詳細資訊，請參閱 ＜ [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=265752)。

## 部署 Microsoft Lync Server 和整合通訊的檢查清單


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>完成了嗎？</th>
<th>作業</th>
<th>主題</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>安裝 Exchange Server 2013 之前，請檢閱系統需求。</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系統需求</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>確認您是否符合安裝的必要條件。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>檢閱整合 Microsoft Lync Server 2013 和 Microsoft Exchange Server 2013 的必要條件。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282082">Exchange Server 2013 整合 Microsoft Lync Server 2013 與 Microsoft 的先決條件</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Unified Communications Managed API (UCMA) 4.0 執行階段是 Exchange 2013 和 Lync Server 2010 和 2013年所需與安裝在安裝期間。若要下載並檢閱 UCMA 4.0 的相關資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=258269">Unified Communications Managed API 4.0 Runtime</a></td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>安裝必要的 Client Access Server 和 Mailbox Server。</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安裝精靈安裝 Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>確認安裝及檢閱伺服器安裝記錄。</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">確認 Exchange 2013 安裝</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>視需要安裝必要的 UM 語言套件。</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">安裝 UM 語言套件</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>建立您組織需要的 SIP URI 撥號對應表數目。</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">建立 UM 撥號對應表</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>設定撥號對應表安全性設定。</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">設定 VoIP 安全性設定</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>設定 Mailbox Server 的同時呼叫數。</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">在信箱伺服器上設定來電的數目</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>設定 Outlook 語音存取號碼和其他設定。</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">管理 UM 撥號對應表</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>將所有 Client Access Server 和 Mailbox Server 新增到各個 SIP URI 撥號對應表。</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">將信箱和用戶端存取伺服器新增至 SIP URI 撥號對應表</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>設定整合通訊的輸出撥接。允許所有電話的 SIP URI 撥號對應都表和 UM 信箱原則連結至那些的撥號對應都表。</p></td>
<td><p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">在 [撥號對應表授權之使用者的通話</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">授權的使用者群組的電話</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>建立所需數量的自動語音應答。</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">建立 UM 自動語音應答</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>設定及配置各個 UM 自動語音應答。</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">設定 UM 自動語音應答</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>針對 UM 建立、匯入及啟用新的 Exchange 憑證，或啟用彼此信任的協力廠商憑證。</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">將信箱和用戶端存取伺服器新增至 SIP URI 撥號對應表</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>針對每部 Client Access Server 和 Mailbox Server，將 UM 啟動模式設定為雙重或 TLS。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">設定信箱伺服器上的啟動模式</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">設定用戶端存取伺服器上的啟動模式</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>重新啟動所有 Exchange 伺服器上的 Microsoft Exchange 整合通訊服務和整合通訊呼叫路由器服務，以便載入必要的憑證。</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">停止 Microsoft Exchange 整合通訊服務</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">啟動 Microsoft Exchange 整合通訊服務</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">停止 Microsoft Exchange Unified Messaging Call Router 服務</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">啟動 Microsoft Exchange Unified Messaging Call Router 服務</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>建立 UM 信箱原則，或設定預設的 UM 信箱原則。</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">建立 UM 信箱原則</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">管理 UM 信箱原則</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>以 SIP 位址為使用者啟用整合通訊功能，並使其與 SIP URI 撥號對應表相連結。</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">啟用使用者的語音信箱</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>檢閱 Lync Server 2013 規劃文件。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282081">計劃</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>安裝及部署 Lync Server 2013。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282051">部署 Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>匯入彼此信任的內部 PKI 或已匯入 Exchange UM Server 的協力廠商憑證。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281863">設定憑證的伺服器</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281865">設定憑證的伺服器上執行 Microsoft Exchange Server Unified Messaging</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>視需要啟動伺服器上的 Lync 服務，以便載入憑證。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282084">啟動伺服器上的服務</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>開啟 Exchange 管理命令介面，並執行位在 %Program Files%\Microsoft\Exchange Server\V15\Scripts 資料夾中的 exchucutil.ps1 指令碼。</p>
<p></p></td>
<td><p><a href="configure-um-to-work-with-lync-server-exchange-2013-help.md">設定 UM 以搭配 Lync Server</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>檢閱 Enterprise Voice 的需求。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281876">Enterprise Voice 的軟體先決條件</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281875">安全性和企業語音設定先決條件</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>部署及設定媒體閘道或中繼伺服器，然後定義同儕。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281872">部署中繼伺服器並定義 Peers</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>在中繼伺服器與一或多個同儕之間設定一個主幹，以提供公用交換電話網路 (PSTN) 連線能力。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281868">設定主幹</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>建立和設定 Lync 撥號對應表，然後建立、定義和關聯正規化規則。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281867">設定撥號對應表</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>設定語音原則，並定義電話用法和外送呼叫路由。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281869">設定語音原則、 PSTN 使用方式記錄和語音路由</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>執行 Exchange 整合公用程式 (ocsumutil.exe)，建立 Outlook 語音存取和自動語音應答的連絡人物件。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281866">設定 Lync Server 2013 與 Microsoft Exchange Server 上的 Unified Messaging 搭配使用</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>定義、部署和設定任何必要的進階 Enterprise Voice 功能。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281871">部署進階企業語音功能</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>為使用者啟用企業語音。輸入線路 URI 和指派語音原則和撥號對應表 Lync。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281873">啟用使用者的企業語音</a></p></td>
</tr>
</tbody>
</table>

