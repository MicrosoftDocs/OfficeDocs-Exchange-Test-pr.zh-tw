---
title: '設定 Outlook 語音存取使用者信箱功能: Exchange Online Help'
TOCTitle: 設定 Outlook 語音存取使用者信箱功能
ms:assetid: 10960bf0-65cf-4d0b-bae5-d203c53662db
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996307(v=EXCHG.150)
ms:contentKeyID: 50553936
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 語音存取使用者信箱功能

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

Outlook語音存取包含兩個介面 ︰ 電話使用者介面 (TUI) 和語音使用者介面 (VUI)。您可以設定已啟用 UM 之使用者 TUI 當使用者存取Exchange 2013中使用整合通訊 (UM) 系統信箱時。當您修改已啟用 UM 之使用者 TUI 設定 UM 信箱原則上的時，所做的變更會影響所有與 UM 信箱原則相關聯的使用者。您可以修改下列 TUI 設定 UM 信箱原則上：

  - 以無 PIN 碼的方式存取語音信箱

  - 以語音回應其他訊息

  - 以 TUI 存取其行事曆

  - 以 TUI 存取目錄

  - 以 TUI 存取其電子郵件

  - 以 TUI 存取其個人連絡人

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只能使用命令介面來修改已啟用 UM 之使用者的 Outlook Voice Access TUI 設定。</td>
</tr>
</tbody>
</table>


如需其他與 UM 信箱原則相關的管理工作，請參閱 [UM 信箱原則程序](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 執行此程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行此程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

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


## 使用命令介面來修改 UM 信箱原則上的 TUI 設定

此範例會設定名為 `MyUMMailboxPolicy` 之 UM 信箱原則上的 TUI 相關設定。

    Set-UMMailbox -identity MyUMMailboxPolicy -AllowSubscriberAccess $true -AllowTUIAccessToCalendar $false -AllowTUIAccessToDirectory $false -AllowTUIAccessToEmail -$true -AllowTUIAccessToPersonalContacts $true

