---
title: '委派角色指派: Exchange 2013 Help'
TOCTitle: 委派角色指派
ms:assetid: ed2d00d9-90c9-49dc-ab8a-cd791569aeed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351237(v=EXCHG.150)
ms:contentKeyID: 50474537
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 委派角色指派

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-02_

管理角色委派可讓角色 assignees 指定的管理角色指派給其他的管理角色群組、 管理角色指派原則、 使用者或萬用安全性群組 (USG)。根據預設，只有組織管理 」 管理角色群組的成員可委派角色指派。部署新安裝的 Microsoft Exchange Server 2013 、 時只安裝Exchange 2013的使用者帳戶為組織管理角色群組的成員。

如果您指派委派的角色給某個角色群組，則該角色群組的任何成員都可以將關聯的管理角色委派給其他角色受託人。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>委派角色指派不會授與角色受託人的權限授與角色、 角色指派給其他人的能力。如果您想要還可讓角色受託人角色來授與的權限，您也必須建立一般角色指派。若要建立一般角色指派，請參閱下列主題：<br />
<a href="manage-role-groups-exchange-2013-help.md">管理角色群組</a><br />
<a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色指派原則</a><br />
<a href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">將角色新增至使用者或 USG</a></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題討論管理角色指派委派。如果您要委派 「 可將成員新增至或移除成員從角色群組，也就是委派的建議的方法，請參閱<a href="manage-role-groups-exchange-2013-help.md">管理角色群組</a>。</td>
</tr>
</tbody>
</table>


如需一般角色指派與委派管理角色指派的相關資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

要尋找與管理的權限相關的其他管理工作嗎？取出[進階權限](advanced-permissions-exchange-2013-help.md)。

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


## 使用命令介面委派管理角色

您可以建立委派角色指派使用同一個預先定義的範圍、 收件者篩選器或伺服器篩選器型範圍、 伺服器清單型範圍和組織單位 (OU) 可用來建立範圍規則或獨佔範圍的範圍。建立一般角色指派和委派角色指派的唯一差異在於*Delegating*轉換到命令加入。如需如何建立角色指派的詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您不能將委派角色指派建立到管理角色指派原則。</td>
</tr>
</tbody>
</table>


此範例會建立委派角色指派，讓「資深系統管理員」角色群組的成員可以指派「郵件收件者」角色給 Exchange 組織中的任一角色受託人。

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admin - Delegate" -Delegating

此範例會建立委派角色指派，讓「資深系統管理員」角色群組的成員只能指派「郵件收件者」角色給 contoso.com 網域銷售\\使用者 OU 中的使用者。

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admins - Delegate" -RecipientOrganizationalUnitScope contoso.com/sales/users -Delegating

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

