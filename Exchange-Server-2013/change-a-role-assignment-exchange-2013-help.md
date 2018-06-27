---
title: '變更角色指派: Exchange 2013 Help'
TOCTitle: 變更角色指派
ms:assetid: 0fa77efc-e393-461f-b3c0-232cc56cee85
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335096(v=EXCHG.150)
ms:contentKeyID: 50472568
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 變更角色指派

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

管理角色指派給角色受託人指派管理角色。您可以透過變更角色指派，控制的角色指派的角色 assignees 可以變更哪些物件。套用至角色指派的管理角色範圍覆寫的角色隱含寫入範圍。不過，角色隱含讀取的範圍仍適用於。您所套用的範圍不能傳回物件的角色隱含讀取範圍外。

如需 Microsoft Exchange Server 2013 中管理角色範圍和指派的相關資訊，請參閱下列主題：

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

要尋找的其他相關角色指派的管理工作嗎？取出[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

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


## 您要執行的工作

## 使用命令介面來啟用或停用角色指派

角色指派已啟用根據預設，這表示相關聯的角色套用至角色受託人將角色指派。如果停用角色指派時，相關聯的角色不會套用至角色受託人。

若要啟用角色指派，請使用下列語法。

    Set-ManagementRoleAssignment <role assignment> -Enabled $true

若要停用角色指派，請使用下列語法。

    Set-ManagementRoleAssignment <role assignment> -Enabled $false

此範例會停用「服務台指派」角色指派。

    Set-ManagementRoleAssignment "Help Desk Assignment" -Enabled $false

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))。

## 使用命令介面來變更角色指派上的管理角色或角色受託人

您無法變更角色指派上指定的角色受託人的管理角色。如果您想要與另一個相關聯的角色指派角色或角色受託人，您必須建立新的角色指派，並刪除舊的角色指派。如需如何新增及移除角色指派的詳細資訊，請參閱下列主題：

  - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [移除使用者或 USG 的角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

如果您已經建立直接指派使用者或萬用安全性群組 (USG)，我們建議您考慮使用管理角色群組和管理角色指派原則。角色群組和指派原則可讓您簡化權限模式並減少管理所需的角色指派的號碼。如需詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 使用命令介面來變更角色指派上的預先定義相對範圍

您可以變更或新增角色指派上預先定義的相對範圍。如果您新增或變更預先定義的範圍，任何先前指定的收件者範圍會移除角色指派。如需預先定義的範圍和及其描述的清單，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

若要在角色指派上變更或新增預先定義的範圍，請使用下列語法。

    Set-ManagementRoleAssignment <assignment name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

此範例會將 John's Assignment 角色指派上的預先定義範圍變更為 MyDistributionGroups。

    Set-ManagementRoleAssignment "John's Assignment" - RecipientRelativeWriteScope MyDistributionGroups

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))。

## 使用命令介面來變更角色指派上的收件者篩選範圍

您可以指定新的收件者篩選器型範圍或變更收件者篩選器型範圍已套用至角色指派。若您要新增的收件者篩選器範圍，任何先前所定義的收件者範圍會移除角色指派。

若要指定新的收件者篩選式範圍，或取代現有的範圍，請使用下列語法。

    Set-ManagementRoleAssignment <assignment name> -CustomRecipientWriteScope <role scope name>

此範例會新增收件者篩選式範圍或將收件者篩選式範圍變更為 Redmond Recipients。

    Set-ManagementRoleAssignment "Redmond Recipient Administrators Assignment" -CustomRecipientWriteScope "Redmond Recipients"

如果您想將同一個收件者篩選器型範圍套用至角色指派但變更用來比對收件者物件的收件者篩選，您需要變更為範圍本身上的收件者篩選器。如需如何變更範圍的詳細資訊，請參閱[角色範圍變更](change-a-role-scope-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))。

## 使用命令介面來變更角色指派上的伺服器篩選或清單式組態範圍

您可以指定新的伺服器篩選或清單型組態範圍或變更已套用至角色指派的範圍。如果您新增或變更組態範圍，任何先前指定的設定範圍已從角色指派。

若要指定新的組態範圍，或取代現有的組態範圍，請使用下列語法。

    Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>

此範例會新增組態範圍或將組態範圍變更為 Redmond Servers。

    Set-ManagementRoleAssignment "Redmond Administrators Assignment" -CustomConfigWriteScope "Redmond Servers"

如果您想將同一個組態範圍套用至角色指派但變更伺服器篩選或範圍中的 \[伺服器\] 清單，您需要變更組態範圍本身擷取。如需如何變更範圍的詳細資訊，請參閱[角色範圍變更](change-a-role-scope-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))。

## 使用命令介面來變更角色指派上的資料庫篩選或清單式組態範圍

您可以指定新的資料庫篩選器或清單型組態範圍或變更已套用至角色指派的範圍。如果您新增或變更組態範圍，任何先前指定的設定範圍已從角色指派。

若要指定新的組態範圍，或取代現有的組態範圍，請使用下列語法。

    Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>

此範例會新增組態範圍或將組態範圍變更為 Redmond Databases。

    Set-ManagementRoleAssignment "Redmond Database Admins" -CustomConfigWriteScope "Redmond Databases"

如果您想將同一個組態範圍套用至角色指派但變更資料庫篩選器或範圍中的 \[資料庫\] 清單，您需要變更組態範圍本身擷取。如需如何變更範圍的詳細資訊，請參閱[角色範圍變更](change-a-role-scope-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))。

## 使用命令介面來變更角色指派上的組織單位

您可以新增新的 OU 或變更已套用至角色指派的 OU。如果您指定新 OU，任何先前指定的收件者範圍會移除角色指派。

若要在角色指派上變更或新增新的 OU，請使用下列語法。

    Set-ManagementRoleAssignment <assignment name> -RecipientOrganizationalUnitScope <OU>

此範例會將 contoso.com 網域中的 Engineering\\Users OU 新增到 Engineering Help Desk 角色指派。

    Set-ManagementRoleAssignment "Engineering Help Desk" -RecipientOrganizationalUnitScope contoso.com/Engineering/Users

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))。

## 使用命令介面來變更獨佔收件者或組態範圍

若要變更獨佔收件者或獨佔組態範圍，您可以使用本節的程序提供在"使用命令介面來變更角色指派，在收件者篩選器範圍""使用命令介面來變更伺服器篩選或清單為基礎的組態範圍在角色指派，"和"使用命令介面來變更資料庫篩選器或在角色指派清單為基礎的組態範圍 」 章節本主題中前面。唯一的不同是獨佔範圍變更後，您必須指定下列 exclusive 參數根據您要變更獨佔收件者範圍或獨佔組態範圍：

  - **獨佔收件者範圍**   使用 *ExclusiveRecipientWriteScope* 參數，而非 *CustomRecipientWriteScope* 參數。

  - **獨佔伺服器和資料庫組態範圍** 使用 *ExclusiveConfigWriteScope* 參數，而非 *CustomConfigWriteScope* 參數。

與一般收件者和組態範圍一樣，如果您新增或變更獨佔範圍，則會取代任何先前定義的收件者或組態範圍。

此範例會變更獨佔收件者寫入範圍。

    Set-ManagementRoleAssignment "Exclusive Executive Users" -ExclusiveRecipientWriteScope "Exclusive Executives"

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))。

