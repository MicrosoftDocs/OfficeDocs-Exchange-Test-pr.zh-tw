---
title: '將角色項目新增至角色: Exchange 2013 Help'
TOCTitle: 將角色項目新增至角色
ms:assetid: 30cd37bc-b3e8-4f39-a8ba-a4c20b1b27b7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335180(v=EXCHG.150)
ms:contentKeyID: 50472797
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將角色項目新增至角色

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-04_

如果您想要授與存取權指令程式，您需要將相關的管理角色項目新增至管理角色。將角色項目新增至角色之後，指派角色的使用者將能夠存取該指令程式。如需管理角色項目在 Microsoft Exchange Server 2013的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

您無法將角色項目新增至內建角色。如果您想要自訂的角色，您必須建立新的角色。如需如何建立新角色的詳細資訊，請參閱[建立角色](create-a-role-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題不會討論如何將未限定範圍的管理角色項目新增至未限定範圍的管理角色。如需如何新增未限定範圍的角色項目，請參閱<a href="add-a-role-entry-to-an-unscoped-top-level-role-exchange-2013-help.md">將角色項目新增至未限定範圍的頂層角色</a>的詳細資訊。</td>
</tr>
</tbody>
</table>


要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理角色」項目。

  - 您必須使用命令介面來執行這些程序。

  - 您要新增至管理角色的角色項目，必須存在該角色的直接上層管理角色中。

  - 本主題使用管線。如需以管線傳送的詳細資訊，請參閱[管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))。

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

## 從上層角色新增單一角色項目

您可以使用下列語法，將角色項目完全依照其出現在上層角色上的方式新增至角色。

    Add-ManagementRoleEntry <child role name>\<cmdlet>

此範例會將 **Set-Mailbox** Cmdlet 新增至「收件者系統管理員」角色。

    Add-ManagementRoleEntry "Recipient Administrators\Set-Mailbox"

此命令會檢查父系角色並如果角色項目存在，將其新增到子系角色。如果角色項目已存在的子角色，您可以包含*Overwrite*參數，來覆寫現有的角色項目。

如需詳細的語法及參數資訊，請參閱 [Add-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351236\(v=exchg.150\))。

## 從上層角色新增單一角色項目，且僅包含特定參數

如果您要從上層角色新增角色項目，但您只想要在子項角色的角色項目中包含特定參數，請使用下列語法。

    Add-ManagementRoleEntry <child role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

此範例會將 **Set-Mailbox** Cmdlet 新增至「服務台」角色，但在子項角色的項目中僅包含 *DisplayName* 和 *EmailAddresses* 參數。

    Add-ManagementRoleEntry "Help Desk\Set-Mailbox" -Parameters DisplayName, EmailAddresses

此命令會檢查父系角色並如果角色項目存在，將其新增到子系角色。如果角色項目已存在的子角色，您可以包含*Overwrite*參數，來覆寫現有的角色項目。

如需詳細的語法及參數資訊，請參閱 [Add-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351236\(v=exchg.150\))。

## 從上層角色新增多個角色項目

如果您想要將一個以上的角色項目新增至角色，您需要擷取存在於您要新增到子系角色，然後將其新增到子系角色父系角色的角色項目清單。為達成此目的，您使用**Get-ManagementRoleEntry**指令程式來擷取在父系角色的角色項目清單。然後您將輸出傳送至**Add-ManagementRoleEntry**指令程式**Get-ManagementRoleEntry**指令程式。若要擷取多個角色項目，您需要使用萬用字元 （\*）。

若要從上層角色將多個項目新增至子項角色，請使用下列語法。

    Get-ManagementRoleEntry <parent role name>\*<partial cmdlet name>* | Add-ManagementRoleEntry -Role <child role name>

此範例會將「郵件收件者」上層角色的 Cmdlet 名稱中包含字串 `Mailbox` 的所有角色項目新增至「西雅圖郵件收件者」子項角色。

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*" | Add-ManagementRoleEntry -Role "Seattle Mail Recipients"

如果子項角色上已存在角色項目，您可以加入 *Overwrite* 參數以覆寫現有的角色項目。

如需擷取管理角色項目清單的詳細資訊，請參閱[檢視角色項目](view-role-entries-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd335210\(v=exchg.150\)) 與 [Add-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351236\(v=exchg.150\))。

