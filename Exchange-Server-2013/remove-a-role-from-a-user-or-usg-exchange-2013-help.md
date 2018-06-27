---
title: '移除使用者或 USG 的角色: Exchange 2013 Help'
TOCTitle: 移除使用者或 USG 的角色
ms:assetid: df3510ef-e0c2-4d3c-81b0-7dc3e70c01a0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351196(v=EXCHG.150)
ms:contentKeyID: 50474444
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除使用者或 USG 的角色

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-02_

管理角色指派給使用者或萬用安全性群組 (USG) 指派管理角色。如果您移除角色指派，指派角色的使用者將不再有可用的 cmdlet 來存取該角色上。如需 Microsoft Exchange Server 2013中的管理角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此程序預估時間： 5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色指派」項目。

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


## 移除管理角色指派

如果您知道要移除的角色指派所用的名稱，請使用下列語法。

    Remove-ManagementRoleAssignment <assignment name>

例如，若要移除 "Tier 2 Help Desk Assignment" 角色指派，請使用下列命令。

    Remove-ManagementRoleAssignment "Tier 2 Help Desk Assignment"

如果不知道角色指派的名稱，可以使用下列語法。

    Get-ManagementRoleAssignment -RoleAssignee <user or USG> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment 

例如，若是要移除使用者 davids 的「郵件收件者」一般角色指派，請使用下列命令。

    Get-ManagementRoleAssignment -RoleAssignee davids -Role "Mail Recipients" -Delegating $false | Remove-ManagementRoleAssignment

