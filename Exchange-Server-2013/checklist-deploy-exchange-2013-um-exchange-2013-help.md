---
title: '檢查清單：部署 Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 檢查清單：部署 Exchange 2013 UM
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 52062536
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢查清單：部署 Exchange 2013 UM

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-03-09_

本檢查清單可協助您在組織中安裝及部署整合通訊 (UM)。

您開始使用這份檢查清單之前，請確定您已熟悉下列概念：

  - [整合通訊](unified-messaging-exchange-2013-help.md)

  - [新的語音信箱功能](new-voice-mail-features-exchange-2013-help.md)

  - [整合通訊的規劃](planning-for-unified-messaging-exchange-2013-help.md)

如需如何部署 UM 和 Microsoft Lync Server 的逐步指引，請參閱[檢查清單： Lync Server 整合 Exchange 2013 UM](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)。

## 部署整合通訊的檢查清單


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>完成了嗎？</th>
<th>Tasks</th>
<th>主題</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>部署及設定電話語音元件。</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">UM 連接至電話系統</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>安裝 Exchange 2013 之前，請檢閱系統需求。</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系統需求</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>確認您是否符合安裝的必要條件。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>安裝必要的 Client Access Server 和 Mailbox Server。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先至少在組織中部署一個 Exchange 2013 Mailbox Server，才能將 VoIP 閘道或 IP PBX 設定為將 UM SIP 和 RTP 流量傳送至 Exchange 2013 Client Access Server。</td>
</tr>
</tbody>
</table>

</td>
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
<td><p>建立組織所需之數量的撥號對應表。</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">建立 UM 撥號對應表</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>設定撥號對應表安全性設定。</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">設定 VoIP 安全性設定</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>設定每部 Client Access Server 和 Mailbox Server 的 UM 啟動模式。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">設定信箱伺服器上的啟動模式</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">設定用戶端存取伺服器上的啟動模式</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>設定 Mailbox Server 的同時呼叫數。</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">在信箱伺服器上設定來電的數目</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>設定 Outlook 語音存取號碼和其他設定。</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">管理 UM 撥號對應表</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>設定整合通訊的輸出撥接。</p></td>
<td><p><a href="authorize-calls-using-dialing-rules-exchange-2013-help.md">授權使用撥號規則的通話</a></p>
<p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">在 [撥號對應表授權之使用者的通話</a></p>
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
<td><p><strong> </strong></p></td>
<td><p>針對 UM 建立、匯入及啟用新的 Exchange 憑證，或啟用彼此信任的協力廠商憑證。此外，在所有 VoIP 閘道、IP PBX 及 SBC 上匯入憑證。</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">將信箱和用戶端存取伺服器新增至 SIP URI 撥號對應表</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>重新啟動所有 Exchange 伺服器上的 Microsoft Exchange 整合通訊服務和整合通訊呼叫路由器服務，以便載入必要的憑證。</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">停止 Microsoft Exchange 整合通訊服務</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">啟動 Microsoft Exchange 整合通訊服務</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">停止 Microsoft Exchange Unified Messaging Call Router 服務</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">啟動 Microsoft Exchange Unified Messaging Call Router 服務</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>建立 UM 信箱原則，或設定預設的 UM 信箱原則。</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">建立 UM 信箱原則</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">管理 UM 信箱原則</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>視需要啟用使用者的整合通訊功能並指派分機號碼和 E.164 號碼。</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">啟用使用者的語音信箱</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>啟用傳入傳真 (選用)。</p></td>
<td><p><a href="enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md">啟用語音信箱使用者接收傳真</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>設定受保護的語音信箱 (選用)。</p></td>
<td><p><a href="protect-voice-mail-exchange-2013-help.md">保護語音信箱</a></p></td>
</tr>
</tbody>
</table>


回到頁首

