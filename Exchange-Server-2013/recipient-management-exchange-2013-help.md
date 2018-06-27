---
title: '收件者管理: Exchange 2013 Help'
TOCTitle: 收件者管理
ms:assetid: 669d602e-68e3-41f9-a455-b942d212d130
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298028(v=EXCHG.150)
ms:contentKeyID: 50473370
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 收件者管理

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

收件者管理 管理角色群組是組成 Microsoft Exchange Server 2013 中角色型存取控制 (RBAC) 權限模型的其中一個內建角色群組。角色群組會有一或多個管理角色指派，其中包含執行指定工作集所需的權限。角色群組的成員擁有指派給該角色群組的管理角色存取權。如需角色群組的詳細資訊，請參閱[了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)。

屬於 收件者管理 角色群組之成員的系統管理員，擁有在 Exchange 2013 組織內建立或修改 Exchange 2013 收件者的系統管理存取權。

這個角色群組相當於 Exchange Server 2007 中的 Exchange 收件者系統管理員角色。

如需有關 RBAC 的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 角色群組成員資格

如果您要新增或移除此角色群組中的成員，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

根據預設，只有組織管理角色群組的成員可以新增或移除此角色群組中的成員。如需如何新增其他角色群組委派的詳細資訊，請參閱 [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的「新增或移除角色群組委派」一節。

您可以使用下列命令來檢視屬於此角色群組成員之使用者或萬用安全性群組 (USG) 的清單。

    Get-RoleGroupMember "Recipient Management"

如需角色群組之成員的詳細資訊，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)中的[View the members of a role group](manage-role-group-members-exchange-2013-help.md)。

## 角色群組自訂

此角色群組預設會獲派管理角色。＜指派給此角色群組的管理角色＞一節中會列出包含的角色。您可以在新增或移除此角色群組的角色指派，以符合組織的需要。

Exchange 2013 所提供的角色群組旨在於符合更細微的工作。將角色指派給角色群組，即可讓該角色群組的成員執行與角色關聯的工作。例如，\[日誌\] 角色會啟用日誌代理程式的管理功能和日誌規則。如需如何將角色指派給角色群組的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

指派給此角色群組的角色會擁有預設的管理範圍。管理範圍決定角色群組的成員可以檢視或修改的 Exchange 物件。您可以變更角色和角色群組之間與指派相關聯的範圍。例如，如果您只想讓角色群組的成員變更特定組織單位下或是特定位置的收件者，則可執行這項操作。如需管理範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

如需如何自訂此角色群組的詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [管理角色群組成員](manage-role-group-members-exchange-2013-help.md)

如果您要建立角色群組並且將指派給此角色群組的部分角色指派給新角色群組，請參閱 [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的＜建立角色群組＞一節。

如果在組織中建立的安全性主體 (例如使用者帳戶) 是由除了 Exchange 系統管理員以外的特定群組所控制，則您可以建立角色群組，並將「建立郵件收件者」角色和「安全性群組建立及成員資格」角色移動到新的角色群組。這樣做可以防止 收件者管理 角色群組的成員建立 Active Directory 物件。不過，他們可以繼續啟用新 Active Directory 物件的郵件功能。 如需分割權限的詳細資訊，請參閱[了解分割權限](understanding-split-permissions-exchange-2013-help.md)。

## 指派給此角色群組的管理角色

下表列出指派給此角色群組的所有管理角色，以及每個角色指派的下列屬性：

  - **一般指派**   可讓角色群組的成員存取相關管管理角色提供的管理角色項目。

  - **委派指派**   讓角色群組的成員能將特定角色指派給其他角色群組、角色指派原則、使用者或 USG。

  - **收件者讀取範圍**   決定角色群組的成員可以從 Active Directory 讀取的收件者物件。

  - **收件者寫入範圍**   決定角色群組的成員可以在 Active Directory 修改的收件者物件。

  - **組態讀取範圍**   決定角色群組的成員可以從 Active Directory 讀取的組態和伺服器物件。

  - **組態寫入範圍**   決定角色群組的成員可以在 Active Directory 修改的組態和伺服器物件。

如需角色指派和管理範圍的詳細資訊，請參閱下列主題：

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

### 指派給此角色群組的管理角色

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>一般指派</th>
<th>委派指派</th>
<th>收件者讀取範圍</th>
<th>收件者寫入範圍</th>
<th>組態讀取範圍</th>
<th>組態寫入範圍</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="distribution-groups-role-exchange-2013-help.md">通訊群組角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">郵件建立收件者角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-recipients-role-exchange-2013-help.md">郵件收件者角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="message-tracking-role-exchange-2013-help.md">郵件追蹤角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="migration-role-exchange-2013-help.md">移轉角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">移動信箱角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-policies-role-exchange-2013-help.md">收件者原則角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">小組信箱角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

