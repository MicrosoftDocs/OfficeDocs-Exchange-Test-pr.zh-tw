---
title: '變更在信箱上的指派原則: Exchange 2013 Help'
TOCTitle: 變更在信箱上的指派原則
ms:assetid: 011690a5-233a-4c03-8842-92276f899a89
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638076(v=EXCHG.150)
ms:contentKeyID: 50472452
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 變更在信箱上的指派原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-08_

您可以變更指派給信箱之管理角色指派原則。當您變更信箱指派原則時時，請變更生效一旦使用者會重新整理連線，例如下次他們登入他們的信箱或開啟信箱選項\] 頁面。如需 Microsoft Exchange Server 2013中指派原則的詳細資訊，請參閱[了解管理角色指派原則](understanding-management-role-assignment-policies-exchange-2013-help.md)。

要尋找相關的權限的其他管理工作嗎？取出[權限](permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色群組」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 EAC 變更信箱的指派原則

1.  在 Exchange 系統管理中心 (EAC)中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  選取使用者或想要變更指派原則的資源信箱後，按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  選取 \[信箱功能\]。

4.  在 \[角色指派原則\] 清單中，選取想要指派給信箱的指派原則後，按一下 \[儲存\]。

## 使用命令介面變更信箱的指派原則

若要變更指派給信箱的指派原則，請使用下列語法。

    Set-Mailbox <mailbox alias or name> -RoleAssignmentPolicy <assignment policy>

此範例會設定信箱 Brian 上「整合通訊使用者」的指派原則。

    Set-Mailbox Brian -RoleAssignmentPolicy "Unified Messaging Users"

## 使用命令介面變更已指派特定指派原則之一組信箱的指派原則

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 同時變更一組信箱的指派原則。</td>
</tr>
</tbody>
</table>


此程序來進行使用管線、 **Where**指令程式及*WhatIf*參數。如需這些概念的詳細資訊，請參閱下列主題：

  - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))

  - [使用命令輸出](working-with-command-output-exchange-2013-help.md)

  - [WhatIf、Confirm 及 ValidateOnly 參數](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

如果您要變更已指派特定原則之一組信箱的指派原則，請使用下列語法。

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<assignment policy to find>" } | Set-Mailbox -RoleAssignmentPolicy <assignment policy to set>

此範例會尋找指派給 Redmond Users - No Voicemail 指派原則的所有信箱，並將指派原則變更為 Redmond Users - Voicemail Enabled。

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled"

此範例包含 *WhatIf* 參數，因此您可以看到將要變更但不會認可任何變更的所有信箱。

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled" -WhatIf

如需詳細的語法及參數資訊，請參閱 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 或 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

