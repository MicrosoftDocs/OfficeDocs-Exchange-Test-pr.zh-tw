---
title: '服務台: Exchange 2013 Help'
TOCTitle: 服務台
ms:assetid: e7958752-22e4-4155-a2fc-948099dec6f7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876949(v=EXCHG.150)
ms:contentKeyID: 50474491
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 服務台

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

服務台 管理角色群組是組成 Microsoft Exchange Server 2013 中角色型存取控制 (RBAC) 權限模型的其中一個內建角色群組。角色群組會有一或多個管理角色指派，其中包含執行指定工作集所需的權限。角色群組的成員擁有指派給該角色群組的管理角色存取權。如需角色群組的詳細資訊，請參閱[了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)。

屬於服務台角色群組成員的使用者可以執行 Exchange 2013 收件者之受限的收件者管理。

Help Desk 角色群組中，根據預設，可讓成員能檢視並修改組織中任何使用者的Outlook Web App選項。這些選項可能包括修改使用者的顯示名稱、 地址、 電話號碼等等。它們不包含不Outlook Web App選項，例如或修改之信箱的大小設定為信箱位於信箱資料庫中可用的選項。

此角色群組的成員只能修改使用者可以修改Outlook Web App選項。這表示如果使用者可以修改其顯示名稱、 Help Desk 角色群組的成員也可以修改該使用者的顯示名稱。不過，如果另一位使用者不允許修改其顯示名稱、 Help Desk 角色群組的成員無法修改該使用者的顯示名稱。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在哪些Outlook Web App選項 Help Desk 角色群組的成員才可以修改要強制Exchange系統管理中心 (EAC) 來限制。如果 Help Desk 角色群組的成員可以存取Exchange管理命令介面，他就可以修改任何Outlook Web App ] 選項的任何使用者。您也應該謹慎考量給進行 Help Desk 角色群組的成員與是否他們應該也會授與存取權以命令介面。</td>
</tr>
</tbody>
</table>


因為如此許多不同類型的組織 Help Desk 角色群組不會啟用任何其他工作。而您可以新增此角色群組建立 Help Desk 角色群組符合組織的需求管理角色。例如，如果您想要能夠管理信箱、 郵件連絡人及擁有郵件功能的使用者之 Help Desk 角色群組的成員，請將 「 郵件收件者管理 」 角色指派給此角色群組。如需如何新增到此角色群組的管理角色的詳細資訊，請參閱本主題稍後的 「 角色群組自訂 」 一節。

如需有關 RBAC 的相關資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 角色群組成員資格

如果您要新增或移除此角色群組中的成員，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

根據預設，只有組織管理角色群組的成員可以新增或移除此角色群組中的成員。如需如何新增其他角色群組委派的詳細資訊，請參閱 [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的「新增或移除角色群組委派」一節。

您可以使用下列命令來檢視屬於此角色群組成員之使用者或萬用安全性群組 (USG) 的清單。

    Get-RoleGroupMember "Help Desk"

如需角色群組之成員的詳細資訊，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)中的[View the members of a role group](manage-role-group-members-exchange-2013-help.md)。

## 角色群組自訂

此角色群組預設會獲派管理角色。＜指派給此角色群組的管理角色＞一節中會列出包含的角色。您可以在新增或移除此角色群組的角色指派，以符合組織的需要。

Exchange 2013 所提供的角色群組旨在於符合更細微的工作。將角色指派給角色群組，即可讓該角色群組的成員執行與角色關聯的工作。例如，\[日誌\] 角色會啟用日誌代理程式的管理功能和日誌規則。如需如何將角色指派給角色群組的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

指派給此角色群組的角色會擁有預設的管理範圍。管理範圍決定角色群組的成員可以檢視或修改的 Exchange 物件。您可以變更角色和角色群組之間與指派相關聯的範圍。例如，如果您只想讓角色群組的成員變更特定組織單位下或是特定位置的收件者，則可執行這項操作。如需管理範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

如需如何自訂此角色群組的詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [管理角色群組成員](manage-role-group-members-exchange-2013-help.md)

如果您要建立角色群組並且將指派給此角色群組的部分角色指派給新角色群組，請參閱 [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的＜建立角色群組＞一節。

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
<td><p><a href="user-options-role-exchange-2013-help.md">使用者選項角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">僅檢視收件者角色</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
</tbody>
</table>

