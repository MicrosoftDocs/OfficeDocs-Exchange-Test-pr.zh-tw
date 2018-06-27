---
title: '從角色移除角色項目: Exchange 2013 Help'
TOCTitle: 從角色移除角色項目
ms:assetid: 4736367a-750f-44d3-8a20-5149bd35e9ff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd297947(v=EXCHG.150)
ms:contentKeyID: 50473051
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從角色移除角色項目

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

管理角色上的管理角色項目決定何種 cmdlets 及參數上可用的管理角色。移除角色項目或角色項目的參數，您可以限制使用者指派管理角色可以執行。如需管理角色項目在 Microsoft Exchange Server 2013的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理角色」項目。

  - 您必須使用命令介面來執行這些程序。

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


## 您要執行的工作

## 移除角色中的單一完整角色項目

當您移除角色中的角色項目，即移除使用者指派角色存取相關指令程式或指令碼的能力。

使用下面的語法移除角色的完整管理角色項目。

    Remove-ManagementRoleEntry <management role>\<management role entry>

這個範例會從「西雅圖伺服器系統管理員」角色中移除 **Enable-MailUser** 指令程式。

    Remove-ManagementRoleEntry "Seattle Server Administrators\Enable-MailUser"

如需詳細的語法及參數資訊，請參閱 [Remove-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351187\(v=exchg.150\))。

## 移除角色中的多個完整角色項目

當您移除角色中的多個角色項目，即移除使用者指派角色存取相關指令程式或指令碼的能力。

若要從角色移除多個角色項目，您需要擷取移除使用**Get-ManagementRoleEntry**指令程式的角色項目清單。然後您需要將傳送到**Remove-ManagementRoleEntry**指令程式輸出。您可以使用萬用字元**Get-ManagementRoleEntry**指令程式來比對多個角色項目。它是不錯的選項以使用*WhatIf*參數，以確認您要移除的正確的角色項目。使用下列語法。

    Get-ManagementRoleEntry <management role>\<role entry with wildcard character> | Remove-ManagementRoleEntry -WhatIf

這個範例會從「西雅圖伺服器系統管理員」角色中移除所有含有文字日誌的角色項目。

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry -WhatIf

當您執行此命令與*WhatIf*參數時，指令程式會傳回所有想要移除的角色項目清單。如果清單看似正確，執行一次沒有*WhatIf*參數的命令移除角色項目。

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd335210\(v=exchg.150\)) 與 [Remove-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351187\(v=exchg.150\))。

## 從角色的角色項目移除參數

當您從角色的角色項目移除參數，指派角色的使用者將無法再使用該參數。

使用下列語法移除角色項目的參數。

    Set-ManagementRoleEntry <management role>\<role entry> -Parameters <parameter 1>,<parameter 2...> -RemoveParameter

這個範例會從「西雅圖伺服器系統管理員」角色的 **Set-Mailbox** 角色項目中移除 *MaxSafeSenders*、*MaxSendSize*、*SecondaryAddress* 和 *UseDatabaseQuotaDefaults* 參數。

    Set-ManagementRoleEntry "Seattle Server Administrators\Set-Mailbox" -Parameters MaxSafeSenders,MaxSendSize,SecondaryAddress,UseDatabaseQuotaDefaults -RemoveParameter

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351162\(v=exchg.150\))。

