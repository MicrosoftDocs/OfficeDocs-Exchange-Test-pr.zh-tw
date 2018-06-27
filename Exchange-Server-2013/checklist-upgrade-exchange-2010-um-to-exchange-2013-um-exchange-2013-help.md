---
title: '檢查清單：將 Exchange 2010 UM 升級至 Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 檢查清單：將 Exchange 2010 UM 升級至 Exchange 2013 UM
ms:assetid: 799bd1b1-a918-4bd8-911e-e6ca08bd7b52
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn169228(v=EXCHG.150)
ms:contentKeyID: 54652593
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢查清單：將 Exchange 2010 UM 升級至 Exchange 2013 UM

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

使用這份檢查清單協助您將 Exchange 2010 整合通訊 (UM) 升級為 Exchange 2013 UM。當您將 Exchange 2010 組織和 UM 部署升級至 Exchange 2013 時，請務必參閱此資訊。如需升級至 Exchange 2013 UM 的逐步指示，請參閱[將 Exchange 2010 UM 升級至 Exchange 2013 UM](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)。

您開始使用這份檢查清單之前，請確定您已熟悉下列概念：

  - [整合通訊的規劃](planning-for-unified-messaging-exchange-2013-help.md)

  - [UM 電話系統整合](telephone-system-integration-with-um-exchange-2013-help.md)

  - [連線至您的電話網路的語音郵件系統](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md)

如需如何從 Exchange 2007 UM 升級至 Exchange 2013 UM 的逐步指引，請參閱[Exchange 2007 UM 升級至 Exchange 2013 UM](upgrade-exchange-2007-um-to-exchange-2013-um-exchange-2013-help.md)。

## 將 Exchange 2010 UM 升級至 Exchange 2013 UM 的檢查清單


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>完成了嗎？</th>
<th>工作</th>
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
<td><p></p></td>
<td><p>確認您是否符合安裝的必要條件。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
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
<td><p></p></td>
<td><p>視需要安裝必要的 UM 語言套件。</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">安裝 UM 語言套件</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>將用於 UM 自訂提示的 Exchange 2010 系統信箱移到 Exchange 2013。</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">在 Exchange 2013 移動信箱</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>即使已移動系統信箱，透過<a href="import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md">匯入及匯出的自訂問候語、 宣告、 功能表及提示</a>，您仍然可以從 Exchange 2010 手動匯入/匯出自訂提示。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>匯出和匯入憑證。</p></td>
<td><p><a href="deploying-certificates-for-um-exchange-2013-help.md">部署 UM 憑證</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>在所有 Exchange 2013 Client Access Server 上設定 UM 啟動模式。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">設定用戶端存取伺服器上的啟動模式</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>在所有 Exchange 2013 Mailbox Server 上設定 UM 啟動模式。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">設定信箱伺服器上的啟動模式</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>建立或設定現有的 UM 撥號對應表。</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">建立 UM 撥號對應表</a></p>
<p><a href="manage-a-um-dial-plan-exchange-2013-help.md">管理 UM 撥號對應表</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>建立或設定現有的 UM IP 閘道。</p></td>
<td><p><a href="create-a-um-ip-gateway-exchange-2013-help.md">建立 UM IP 閘道器</a></p>
<p><a href="manage-a-um-ip-gateway-exchange-2013-help.md">管理 UM IP 閘道器</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>建立 UM 群組搜尋。</p></td>
<td><p><a href="create-a-um-hunt-group-exchange-2013-help.md">建立 UM 群組搜尋</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>建立或設定 UM 自動語音應答。</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">建立 UM 自動語音應答</a></p>
<p><a href="manage-a-um-auto-attendant-exchange-2013-help.md">管理 UM 自動語音應答</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>建立或設定 UM 信箱原則。</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">建立 UM 信箱原則</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">管理 UM 信箱原則</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>將現有的啟用 UM 的信箱移至 Exchange 2013。</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">在 Exchange 2013 移動信箱</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>為新的使用者啟用 UM，或對現有已啟用 UM 的使用者進行設定。</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">啟用使用者的語音信箱</a></p>
<p><a href="manage-voice-mail-settings-for-a-user-exchange-2013-help.md">管理使用者的語音郵件設定</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>將 VoIP 閘道、IP PBX 及已啟用 SIP 的 PBX 設定為傳送所有來電至 Exchange 2013 Client Access Server。</p></td>
<td><p><a href="configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md">支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項</a> <a href="connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md">連線至 UM VoIP 閘道、 IP PBX 或工作階段邊界控制器</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>在 Exchange 2010 UM Server 上停用自動答錄。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296335">停用 Exchange 2010 整合通訊</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>從撥號對應表中移除 Exchange 2010 UM Server。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296336">從撥號對應表中移除 UM</a></p></td>
</tr>
</tbody>
</table>

