---
title: '使用資料庫範圍控制自動信箱發佈: Exchange 2013 Help'
TOCTitle: 使用資料庫範圍控制自動信箱發佈
ms:assetid: 8eaff177-2251-4c8b-8570-c91a77d0a6fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff628332(v=EXCHG.150)
ms:contentKeyID: 50473714
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用資料庫範圍控制自動信箱發佈

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

自動信箱發佈是 Microsoft Exchange Server 2013 中的功能，可在您未明確指定資料庫時，隨機選取信箱資料庫來儲存新信箱或移動的信箱。當您想要讓新手系統管理員或服務台員工建立信箱，且不需要他們知道應在哪些信箱資料庫上建立信箱時，此功能會很有用。

您可以使用資料庫管理範圍，控制可由自動信箱發佈選取哪些信箱資料庫。當您將資料庫範圍套用至系統管理員時，只有符合已定義資料庫範圍的資料庫可供系統管理員使用。由於自動信箱發佈使用目前使用者的內容，因此也會受限於套用至系統管理員的資料庫範圍。

如需自動信箱發佈、資料庫範圍和角色指派的詳細資訊，請參閱下列主題：

  - [自動信箱發佈](automatic-mailbox-distribution-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

要尋找與範圍相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 此程序預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理範圍」項目。

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


## 該怎麼做？

## 步驟 1：建立資料庫範圍

在此步驟中，決定要將哪些資料庫包含在資料庫範圍中。此外，決定是否要指定資料庫的靜態清單，或者是否要建立只包含符合所指定準則之資料庫的資料庫篩選器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>資料庫範圍與相關聯的角色指派只適用於連線到執行 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 的伺服器的使用者或更新版本或Exchange 2013。如果指派資料庫範圍與相關聯的角色指派的使用者連線至預先Exchange 2010 SP1 的伺服器、 角色指派不會套用至該使用者，並不會授與使用者角色指派所提供的任何權限。</td>
</tr>
</tbody>
</table>


## 使用資料庫清單範圍

如果要定義應包含在此範圍中的信箱資料庫靜態清單，請使用資料庫清單。使用下列語法，可建立資料庫清單範圍。

    New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>

這個範例會建立只套用至資料庫 Database 1、Database 2 和 Database 3 的範圍。

    New-ManagementScope -Name "Accounting databases" -DatabaseList "Database 1", "Database 2", "Database 3"

如需詳細的語法及參數資訊，請參閱 [New-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd335137\(v=exchg.150\))。

## 使用資料庫篩選器範圍

如果要建立只包含符合所指定準則之資料庫的動態資料庫範圍，請使用資料庫篩選器。如果您不想在建立資料庫範圍後管理它，且您已為組織定義可識別特定信箱資料庫集合的標準值，這會非常有用。

如需可篩選資料庫內容的清單，請參閱 [了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

使用下列語法，可建立資料庫篩選器範圍。

    New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>

這個範例會建立一個範圍，此範圍包括資料庫 **Name** 屬性中包含 "ACCT" 字串的所有資料庫。

    New-ManagementScope -Name "Accounting Databases" -DatabaseRestrictionFilter { Name -Like '*ACCT*' }

如需詳細的語法及參數資訊，請參閱 [New-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd335137\(v=exchg.150\))。

## 步驟 2：將資料庫範圍新增至管理角色指派

在您建立範圍之後，必須將其新增至新的或現有的管理角色指派。我們建議您使用管理角色群組來控制管理權限，因此，此步驟中的範例使用稱為「會計系統管理員」的範例角色群組。如需如何建立角色群組的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

在您指派角色給具有資料庫範圍的角色群組後，角色群組成員將只能在包含在範圍中的資料庫上建立信箱，或將信箱移至包含在範圍中的資料庫。

如需可以指派給角色群組的內建角色清單，請參閱[內建管理角色](built-in-management-roles-exchange-2013-help.md)。

## 新增角色指派

如果您已建立角色群組且需要新增角色至其中，請使用此程序。

請使用下列語法，在您要指派的管理角色與新角色群組之間，以新的資料庫範圍建立角色指派。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <database scope name>

下列範例使用「會計資料庫」資料庫範圍，在「郵件收件者」和「建立郵件收件者」與「會計系統管理員」角色群組之間建立角色指派。

    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipients" -CustomConfigWriteScope "Accounting Databases"
    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipient Creation" -CustomConfigWriteScope "Accounting Databases"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 修改現有的角色指派

如果您現有的角色群組與您要套用新資料庫範圍的角色之間已經有角色指派，請使用此程序。

此程序使用管線。如需詳細資訊，請參閱[管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))。

請使用下列語法，在您要套用資料庫範圍的管理角色與現有角色群組之間修改角色指派。

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> | Set-ManagementRoleAssignment -CustomConfigWriteScope <database scope name>

此範例會將「會計資料庫」資料庫範圍，新增至指派給「會計系統管理員」角色群組的「郵件收件者」和「建立郵件收件者」角色。

    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipients" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"
    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipient Creation" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\)) 或 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))。

## 步驟 3：新增成員至角色群組 (如果適用)

如果您要新增成員至角色群組，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您新增成員至此角色群組，以限制可在其上建立使用者或將信箱移至其中的資料庫，請確認它們不是可授與額外權限之其他角色群組的成員。</td>
</tr>
</tbody>
</table>


## 步驟 4：將成員從角色群組中移除 (如果適用)

若您已新增成員至新的角色群組，該角色群組限制可在其上建立信箱或將信箱移至其中的資料庫，而這些成員是具有額外權限之其他角色群組的成員，請將它們從舊的角色群組中移除。如需詳細資訊，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

