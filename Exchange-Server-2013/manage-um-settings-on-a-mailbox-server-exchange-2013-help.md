---
title: '管理信箱伺服器上的 UM 設定: Exchange 2013 Help'
TOCTitle: 管理信箱伺服器上的 UM 設定
ms:assetid: 6df4853d-21d2-473f-b0ca-ebc996d8794a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998815(v=EXCHG.150)
ms:contentKeyID: 50554005
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMServerPropertiesPropertyPage
ms.translationtype: MT
---

# 管理信箱伺服器上的 UM 設定

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-11_

安裝執行 Microsoft Exchange 整合通訊服務的 Mailbox Server 之後，就可以設定數個選項，包括同時呼叫數、TCP 和傳輸層安全性 (TLS) 接聽通訊埠、狀態，以及 UM 啟動模式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>則不需要的信箱伺服器新增至 UM 撥號對應表之前它可處理呼叫的整合通訊 (UM)，除了時您正在整合 UM 與 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server。根據預設，在組織中的所有 Mailbox server 都可用來接聽來電。</td>
</tr>
</tbody>
</table>


關於與整合通訊和信箱伺服器相關的其他管理工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「Mailbox server (UM Service)」項目。

  - 確認信箱伺服器已經安裝完成，無論是在用戶端存取伺服器的同一部電腦上或位於其他電腦上。

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

## 使用命令介面設定信箱伺服器上的整合通訊內容

此範例會從所有工作階段初始通訊協定 (SIP) 撥號對應表中移除名為 `MyMailboxServer` 的信箱伺服器r。

    Set-UMService -Identity MyMailboxServer -DialPlans $null

此範例會將名為 `MyMailboxServer` 的信箱伺服器r，新增到名稱為 `MySIPDialPlanName` 的 UM SIP 撥號對應表中，同時設定傳入語音呼叫數目的上限。

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -MaxCalls 150 

此範例會在名為 `MyUMServer` 的信箱伺服器上將啟動模式設為雙重模式。

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -UMStartUpMode -Dual 

## 使用命令介面檢視信箱伺服器內容

此範例會顯示所有信箱伺服器的清單。

    Get-UMService

此範例則會顯示名為 `MyMailboxServer` 的信箱伺服器的格式化內容清單。

    Get-UMService -Identity MyMailboxServer | Format-List

