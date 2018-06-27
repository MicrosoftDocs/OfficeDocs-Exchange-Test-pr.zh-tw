---
title: '將角色新增至使用者或 USG: Exchange 2013 Help'
TOCTitle: 將角色新增至使用者或 USG
ms:assetid: ae5608de-a141-4714-8876-bce7d2a22cb5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351056(v=EXCHG.150)
ms:contentKeyID: 50473985
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將角色新增至使用者或 USG

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

管理角色指派可將管理角色指派給使用者或萬用安全性群組 (USG)。將角色指派給使用者或 USG，您就可以讓這些使用者執行工作取決於 cmdlet 或指令碼及它們在 「 管理 」 角色上定義的參數。

如果您要將角色指派給管理角色群組或管理角色指派原則，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [管理角色指派原則](manage-role-assignment-policies-exchange-2013-help.md)

如果您要將成員新增至角色群組或將角色指派原則指派給使用者，請參閱下列主題：

  - [管理角色群組成員](manage-role-group-members-exchange-2013-help.md)

  - [變更在信箱上的指派原則](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

如需相關資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色指派」項目。

  - 您必須使用命令介面來執行這些程序。

  - 雖然您可以角色直接指派給使用者和 Usg，授與權限給系統管理員和使用者的建議的方法是使用管理角色群組和管理角色指派原則。當您使用角色群組和指派原則時，會簡化權限模型。

  - 角色指派的 additive。這表示他們正在評估當中的所有角色會一起都加入。如果兩種角色指派給使用者和一個角色包含指令程式，但其他不，仍會提供給使用者指令程式。
    
    根據預設，角色指派不授與重新指派給其他使用者的角色。若要讓使用者將角色指派給其他使用者或 Usg，請參閱[委派角色指派](delegate-role-assignments-exchange-2013-help.md)。

  - 如果您建立工作分派範圍、 範圍會覆寫的角色隱含寫入範圍。不過，角色隱含讀取的範圍仍適用於。新的範圍不能傳回物件的角色隱含讀取範圍外。如需詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

  - 本主題中的所有程序可用於將角色指派給 USG *SecurityGroup*參數。如果您想要指派給特定使用者的角色，使用*User*參數，而不是*SecurityGroup*參數。每個命令的所有其他語法不相同。

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

## 建立沒有範圍的角色指派

您可以建立角色指派任何範圍。當您這樣做時，不明確的讀取和隱含寫入範圍的角色套用。

使用下列語法來指派角色給 USG 且不使用任何範圍。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name>

這個範例會將 Exchange Server 角色指派給 SeattleAdmins USG。

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 使用預先定義的相對範圍建立角色指派

如果預先定義的相對範圍符合您的業務需求，您可以將該範圍套用至角色指派，而不是建立自訂範圍。如需預先定義的範圍和及其描述的清單，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

使用下列語法來指派角色給 USG，並使用預先定義的範圍。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

這個範例會將 Exchange Server 角色指派給 SeattleAdmins USG，並套用「組織」預先定義範圍。

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers" -RecipientRelativeWriteScope Organization

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 使用以收件者篩選器為基礎的範圍建立角色指派

如果您建立收件者篩選器為基礎的範圍，且想要使用與角色指派您需要用來使用*CustomRecipientWriteScope*參數將角色指派給 USG 命令中包含範圍。如果您使用*CustomRecipientWriteScope*參數，您無法使用*RecipientOrganizationalUnitScope*參數。

您可以將範圍新增至角色指派之前，您需要建立 web 應用程式。如需詳細資訊，請參閱[建立規則或獨佔範圍](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

使用下列語法來指派角色給 USG，並使用以收件者篩選器為基礎的範圍。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -CustomRecipientWriteScope <role scope name>

這個範例會將 Mail Recipients 角色指派給 Seattle Recipient Admins USG，並套用 Seattle Recipients 範圍。

    New-ManagementRoleAssignment -Name "Mail Recipients_Seattle Recipient Admins" -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -CustomRecipientWriteScope "Seattle Recipients"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 使用伺服器或資料庫篩選器，或以清單為基礎的組態範圍建立角色指派

如果您建立伺服器或資料庫篩選器，或以清單為基礎的組態範圍，且想要將此範圍用於角色指派，則在用於指派角色給 USG 的命令中，您必須使用 *CustomConfigWriteScope* 參數來包含該範圍。

您可以將範圍新增至角色指派之前，您需要建立 web 應用程式。如需詳細資訊，請參閱[建立規則或獨佔範圍](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

使用下列語法來指派角色給 USG，並使用組態範圍。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -CustomConfigWriteScope <role scope name>

這個範例會將 Exchange Server 角色指派給 MailboxAdmins USG，並套用「信箱伺服器」範圍。

    New-ManagementRoleAssignment -Name "Exchange Servers_MailboxAdmins" -SecurityGroup MailboxAdmins -Role "Exchange Servers" -CustomConfigWriteScope "Mailbox Servers"

上述範例顯示如何新增伺服器組態範圍的角色指派。若要新增資料庫組態範圍的語法為相同。您指定資料庫範圍，而不是伺服器範圍的名稱。

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 建立具有 OU 範圍的角色指派

如果您想要的範圍的角色寫入範圍至組織單位 (OU)，您可以指定 OU *RecipientOrganizationalUnitScope*參數中直接。如果您使用*RecipientOrganizationalUnitScope*參數，您無法使用*CustomRecipientWriteScope*參數。

使用下列語法來指派角色給 USG，並將角色的寫入範圍限制為特定的 OU。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -RecipientOrganizationalUnitScope <OU>

這個範例會將 Mail Recipients 角色指派給 SalesRecipientAdmins USG，並將指派的範圍設定為 contoso.com 網域中的 sales/users OU。

    New-ManagementRoleAssignment -Name "Mail Recipients_SalesRecipientAdmins" -SecurityGroup SalesRecipientAdmins -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 建立具有獨佔收件者或組態範圍的角色指派

建立獨佔收件者或組態範圍的獨佔角色指派，可以使用 \[建立收件者篩選器型範圍的角色指派和建立角色指派與伺服器或資料庫的篩選器或清單型組態範圍\] 區段中所提供的相同程序。唯一的不同是當您建立角色指派具有獨佔範圍時，您必須指定下列 exclusive 參數根據您正在使用獨佔收件者範圍或獨佔組態範圍：

  - **獨佔收件者範圍**   使用 *ExclusiveRecipientWriteScope* 參數，而非 *CustomRecipientWriteScope* 參數。

  - **獨佔組態範圍**   使用 *ExclusiveConfigWriteScope* 參數，而非 *CustomConfigWriteScope* 參數。

當您執行此程序時，指派角色的角色 assignees 可以針對執行動作獨佔範圍中包含的物件。如需獨佔範圍的詳細資訊，請參閱[了解獨佔範圍](understanding-exclusive-scopes-exchange-2013-help.md)。

您不能建立同時具有獨佔範圍和標準範圍的角色指派。

這個範例會將 Mail Recipients 角色指派給 Protected User Admins USG，並套用 Protected Users 獨佔範圍。

    New-ManagementRoleAssignment -Name "Mail Recipients_Protected User Admins" -SecurityGroup "Protected User Admins" -Role "Mail Recipients" -ExclusiveRecipientWriteScope "Protected Users"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

