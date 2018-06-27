---
title: '設定 Outlook 語音存取使用者信箱功能: Exchange Online Help'
TOCTitle: 設定 Outlook 語音存取使用者信箱功能
ms:assetid: a56bfd75-7bc5-49b9-b098-06855a720dcd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124030(v=EXCHG.150)
ms:contentKeyID: 50554068
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 語音存取使用者信箱功能

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

使用者存取的整合通訊 (UM) 系統使用Outlook語音存取時使用電話使用者介面 (TUI) 設定。當您修改已啟用 UM 之使用者 TUI 組態設定時，您可以修改內容及已啟用 UM 之使用者的信箱上其值。

您可以為已啟用 UM 的使用者變更以下 TUI 設定：

  - 允許使用者存取

  - 允許對行事曆的 TUI 存取

  - 允許對電子郵件的 TUI 存取

  - 允許自動語音辨識

如需與 UM 使用者相關的其他管理工作，請參閱[設定 Outlook 語音存取使用者信箱功能](set-mailbox-features-for-an-outlook-voice-access-user-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 執行這些程序之前，請確認現有Exchange收件者已啟用整合通訊和語音信箱。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

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


## 使用命令介面修改已啟用 UM 之單一使用者的 TUI 設定

本範例會讓 Tony Smith 這位已啟用 UM 的使用者，能夠使用 TUI 來存取行事曆和電子郵件。

    Set-UMMailbox -Identity tony@contoso.com TUIAccessToCal True -TUIAccessToEmail True -OperatorNumber 111111 -DisableMissedCallNotification False -AnonCallBlock True

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用者的 TUI 設定也包含可在 UM 信箱原則。修改 TUI 設定 UM 信箱原則上的會影響所有與 UM 信箱原則相關聯的使用者。如需如何修改 TUI 設定 UM 信箱原則的詳細資訊，請參閱<a href="set-mailbox-features-for-outlook-voice-access-users-exchange-2013-help.md">設定 Outlook 語音存取使用者信箱功能</a>。</td>
</tr>
</tbody>
</table>

