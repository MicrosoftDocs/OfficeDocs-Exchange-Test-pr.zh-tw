---
title: '管理的用戶端存取伺服器上的 UM 設定: Exchange 2013 Help'
TOCTitle: 管理的用戶端存取伺服器上的 UM 設定
ms:assetid: 08667911-fa86-404e-84b1-65cedd94d579
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673507(v=EXCHG.150)
ms:contentKeyID: 50553931
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理的用戶端存取伺服器上的 UM 設定

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-09_

在您安裝執行 Microsoft Exchange Unified Messaging Call Router 服務的 Client Access Server 之後，您可以設定許多選項，包括同時來電數、TCP 和傳輸層安全性 (TLS) 接聽埠、狀態和啟動模式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>則不需要用戶端存取伺服器要新增至 UM 撥號對應表計劃之前它可處理呼叫的整合通訊 (UM)，除了時您正在整合 UM 與 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server。根據預設，在組織中的所有用戶端存取伺服器可用來接聽來電。</td>
</tr>
</tbody>
</table>


如需其他與整合通訊和用戶端存取伺服器相關的工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「用戶端存取伺服器 (UM 呼叫路由器服務)」項目。

  - 確認用戶端存取伺服器已經安裝完成，無論是在信箱伺服器的同一部電腦上或位於其他電腦上。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用命令介面以在 Client Access Server 設定整合通訊內容

此範例會從所有工作階段初始通訊協定 (SIP) 撥號對應表中移除名為 `MyClientAccessServer` 的 Client Access Server。

    Set-UMCallRouterSettings -DialPlans $null - Server MyClientAccessServer

此範例會將名為 `MyClientAccessServer` 的 Client Access Server 新增到名為 `MySIPDialPlan` 的 SIP 撥號對應表中，同時設定傳入語音呼叫數目的上限。

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -MaxCalls 150 -Server MyClientAccessServer

此範例會在名為 `MyClientAccessServer` 的 Client Access Server 上將 SIP TCP 接聽埠設定為 5077，以及將啟動模式設定為雙重模式。

    Set-UMCallRouterSettings  -Server MyClientAccessServer-SipTCPListeningPort 5077 -UMStartUpMode -Dual 

## 使用命令介面來檢視 Client Access Server 內容

此範例會顯示所有 Client Access Server 的清單。

    Get-UMCallRouterSettings

此範例則會顯示 Client Access Server 的格式化內容清單。

    Get-UMCallRouterSettings | Format-List

