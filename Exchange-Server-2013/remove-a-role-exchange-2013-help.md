---
title: '移除角色: Exchange 2013 Help'
TOCTitle: 移除角色
ms:assetid: 2fb6f453-f37a-4636-8353-3f9927f81298
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335178(v=EXCHG.150)
ms:contentKeyID: 50472789
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除角色

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

可以從您的組織移除不再需要的管理角色。您只可以移除您所建立的管理角色。無法移除內建管理角色。如需 Microsoft Exchange Server 2013中的管理角色的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理角色」項目。

  - 您必須使用命令介面來執行這些程序。

  - 您可以移除管理角色之前，您必須移除其所有管理角色指派。如需如何移除角色指派的詳細資訊，請參閱[移除使用者或 USG 的角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)。

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

## 移除沒有子項角色的管理角色

若要移除沒有子項角色的角色，請使用下列語法。

    Remove-ManagementRole <role name>

此範例會移除「西雅圖伺服器系統管理員」角色。

    Remove-ManagementRole "Seattle Server Administrators"

如需詳細的語法及參數資訊，請參閱 [Remove-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351170\(v=exchg.150\))。

## 移除有子項角色的管理角色

如果您想要移除的角色具有子系角色，您必須也移除所有子系角色。如果您嘗試移除具有除非您使用*Recurse*參數的子系角色的角色，收到錯誤訊息。如果您使用*Recurse*參數移除角色時，會移除您指定的角色和其所有子系角色。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用<em>Recurse</em>參數時，也會移除指定您想要移除之角色的所有子系角色。請確定您知道的何種角色將會移除才可執行此命令。</td>
</tr>
</tbody>
</table>


若要確定您移除您要移除的角色，使用*WhatIf*參數與您的命令來確認其正確。使用下列語法。

    Remove-ManagementRole <role name> -Recurse -WhatIf

*WhatIf*參數執行命令但不認可所有的變更與哪些角色就已移除的報告。如需關於*WhatIf*切換，請參閱[WhatIf、Confirm 及 ValidateOnly 參數](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)。

確認 \[僅限您想要移除的角色將會移除之後，請執行含*WhatIf*參數在同一個命令。此範例會移除倫敦系統管理員角色及其所有子系角色。

    Remove-ManagementRole "London Administrators" -Recurse

如需詳細的語法及參數資訊，請參閱 [Remove-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351170\(v=exchg.150\))。

## 移除未限定範圍的管理角色

若要移除未限定範圍的角色，可以使用本主題前述所移除管理角色與任何子系角色和移除管理角色與子系角色中所提供的相同程序。唯一的不同是當您移除未限定範圍的角色，您必須指定*UnScopedTopLevel*交換器當您執行命令。此範例會移除未限定範圍的角色及其所有子系角色。

    Remove-ManagementRole "Custom IT Scripts" -Recurse -UnScopedTopLevel

與移除其他角色一樣，您應該使用 *WhatIf* 參數來確認移除的是正確角色。

如需詳細的語法及參數資訊，請參閱 [Remove-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351170\(v=exchg.150\))。

