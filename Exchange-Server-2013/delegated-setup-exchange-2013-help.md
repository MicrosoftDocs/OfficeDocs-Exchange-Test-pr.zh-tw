---
title: '委派安裝: Exchange 2013 Help'
TOCTitle: 委派安裝
ms:assetid: 49362059-e53f-4135-ad2b-9edfbfff9a1e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876881(v=EXCHG.150)
ms:contentKeyID: 50473066
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 委派安裝

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

委派安裝 管理角色群組是組成 Microsoft Exchange Server 2013 中角色型存取控制 (RBAC) 權限模型的其中一個內建角色群組。角色群組會有一或多個管理角色指派，其中包含執行指定工作集所需的權限。角色群組的成員擁有指派給該角色群組的管理角色存取權。如需角色群組的詳細資訊，請參閱[了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)。

身為「委派安裝」角色群組成員的系統管理員，可部署先前已由 Exchange 2013 角色群組的成員提供的 組織管理 伺服器。

委派安裝 」 角色群組的成員可以只部署Exchange 2013伺服器。他們無法管理伺服器之後已部署。若要管理伺服器已部署之後，使用者必須[伺服器管理](server-management-exchange-2013-help.md)角色群組的成員。

如需有關 RBAC 的相關資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 角色群組成員資格

如果您要新增或移除此角色群組中的成員，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

根據預設，只有組織管理角色群組的成員可以新增或移除此角色群組中的成員。如需如何新增其他角色群組委派的詳細資訊，請參閱 [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的「新增或移除角色群組委派」一節。

您可以使用下列命令來檢視屬於此角色群組成員之使用者或萬用安全性群組 (USG) 的清單。

    Get-RoleGroupMember "Delegated Setup"

如需角色群組之成員的詳細資訊，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)中的[View the members of a role group](manage-role-group-members-exchange-2013-help.md)。

## 角色群組自訂

此角色群組預設會獲派管理角色。＜指派給此角色群組的管理角色＞一節中會列出包含的角色。您可以在新增或移除此角色群組的角色指派，以符合組織的需要。

Exchange 2013 所提供的角色群組旨在於符合更細微的工作。將角色指派給角色群組，即可讓該角色群組的成員執行與角色關聯的工作。例如，\[日誌\] 角色會啟用日誌代理程式的管理功能和日誌規則。如需如何將角色指派給角色群組的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

指派給此角色群組的角色會擁有預設的管理範圍。管理範圍決定角色群組的成員可以檢視或修改的 Exchange 物件。您可以變更角色和角色群組之間與指派相關聯的範圍。例如，如果您只想讓角色群組的成員變更特定組織單位下或是特定位置的收件者，則可執行這項操作。如需管理範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

如需如何自訂此角色群組的詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [管理角色群組成員](manage-role-group-members-exchange-2013-help.md)

如果您要建立角色群組並且將指派給此角色群組的部分角色指派給新角色群組，請參閱 [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的＜建立角色群組＞一節。

## 其他權限

管理角色指派給角色群組主要是取決於委派安裝 」 角色群組的成員授與的權限。不過，您必須執行的所有工作並都涵蓋管理角色。這是因為某些工作發生外部Exchange管理工具與因此不會套用的 RBAC 權限模型。這些工作，由委派安裝 」 角色群組新增至特定Active Directory物件的存取控制清單 (Acl) 所提供的權限。

下列工作是透過 Active Directory 物件的 ACL，而非透過指派給「委派安裝」角色群組的管理角色來獲得權限：

  - 部署先前已由 組織管理 角色群組的成員提供的伺服器。

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
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">僅檢視設定角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
</tbody>
</table>

