---
title: '停用的 Outlook 語音存取使用者所選取的功能: Exchange Online Help'
TOCTitle: 停用的 Outlook 語音存取使用者所選取的功能
ms:assetid: 37421edf-af60-4ca9-9e8b-262b8b851607
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg602126(v=EXCHG.150)
ms:contentKeyID: 50553962
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用的 Outlook 語音存取使用者所選取的功能

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

Outlook語音存取包含兩個介面 ︰ 電話的使用者介面 (TUI) 和語音使用者介面 (VUI)。根據預設，當使用者撥入Outlook語音存取他們可以存取其行事曆、 電子郵件、 及個人連絡人及搜尋目錄。您可以使用命令介面來防止使用者存取其信箱Outlook語音存取時存取一或多個這些功能。當您修改整合通訊 (UM) 信箱原則上的Outlook語音存取功能時，您的變更會影響所有與 UM 信箱原則相關聯的使用者。

您可以在 UM 信箱原則上，停用使用者對下列 Outlook 語音存取功能的存取：

  - 行事曆

  - Directory

  - Email

  - 個人連絡人

如需其他與 UM 信箱原則相關的管理工作，請參閱 [UM 信箱原則程序](um-mailbox-policy-procedures-exchange-2013-help.md)。

您也可以使用命令介面來停用單一的啟用 UM 之使用者的信箱上的Outlook語音存取功能。當您這麼做時，將僅針對該使用者停用功能。雖然您無法停用單一使用者的 UM 信箱原則找到的所有Outlook語音存取功能，您可以停都用存取其行事曆和電子郵件。

如需與 UM 信箱相關的其他管理工作，請參閱[使用者的語音信箱](voice-mail-for-users-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只可以使用命令介面，在 UM 信箱原則上或在單一已啟用 UM 之使用者的信箱上，為已啟用 UM 的使用者修改 Outlook Voice Access 功能。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已啟用 UM 的使用者。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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

## 使用命令介面在 UM 信箱原則上停用已啟用 UM 之使用者的選定 Outlook 語音存取功能

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

此範例會防止與名為 `MyUMMailboxPolicy` 之 UM 信箱原則關聯的使用者，在撥入 Outlook Voice Access 時存取其行事曆。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToCalendar $false

此範例會防止與名為 `MyUMMailboxPolicy` 之 UM 信箱原則關聯的使用者，在撥入 Outlook Voice Access 時存取其目錄。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToDirectory $false

此範例會防止與名為 `MyUMMailboxPolicy` 之 UM 信箱原則關聯的使用者，在撥入 Outlook Voice Access 時存取其電子郵件。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToEmail -$false

此範例會防止與名為 `MyUMMailboxPolicy` 之 UM 信箱原則關聯的使用者，在撥入 Outlook Voice Access 時存取其個人連絡人。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToPersonalContacts $false

## 使用命令介面在單一已啟用 UM 之使用者的信箱上停用選取的 Outlook 語音存取功能

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

此範例會在使用者撥入 Outlook 語音存取時，停用對名為 tony@contoso.com 之 UM 信箱上行事曆的存取。

    Set-UMMailbox -id tony@contoso.com -TUIAccessToCalendarEnabled $false

此範例會在使用者撥入 Outlook Voice Access 時，停用對名為 tony@contoso.com 之 UM 信箱上電子郵件的存取。

    Set-UMMailbox -id tony@contoso.com -TUIAccessToEmailEnabled $false

