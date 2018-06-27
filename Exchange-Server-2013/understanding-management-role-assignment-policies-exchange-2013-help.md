---
title: '了解管理角色指派原則: Exchange 2013 Help'
TOCTitle: 了解管理角色指派原則
ms:assetid: 25913e43-326a-4371-90b5-021a35f100fe
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638100(v=EXCHG.150)
ms:contentKeyID: 50472839
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解管理角色指派原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

*管理角色指派原則*是一組一或多個使用者管理角色可讓使用者能管理自己 Microsoft Exchange Server 2013信箱和通訊群組設定。角色指派原則是在Exchange 2013中的角色型存取控制 (RBAC) 權限模型的一部分，可讓您控制哪些特定信箱及通訊群組組態設定可以修改您的使用者。不同的使用者群組可以有角色指派原則專門給他們。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題著重於進階 RBAC 功能。如果您要管理基本 Exchange 2013 權限，例如使用 Exchange 系統管理中心 (EAC) 新增和移除角色群組的成員、建立和修改角色群組，或建立和修改角色指派原則，請參閱<a href="permissions-exchange-2013-help.md">權限</a>。</td>
</tr>
</tbody>
</table>


如需有關 RBAC 的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

**目錄**

Role assignment policy layers

Default and explicit role assignment policies

Using role assignment policies

Role assignment policy management

## 角色指派原則層

以下清單說明構成角色指派原則模型的各種層：

  - **信箱**  單一角色指派原則指派給信箱。當信箱指派角色指派原則時指派管理角色和角色指派原則之間會套用至信箱。這會授與信箱之所有權限的管理角色所提供。

  - **管理角色指派原則**  *管理角色指派原則*是Exchange 2013中的特殊物件。使用者與相關聯的角色指派原則時所建立信箱，或是變更角色指派原則的信箱上。這也是您要使用者管理角色指派。在角色指派原則的所有角色的組合會定義使用者可以管理的所有項目在其信箱或通訊群組。

  - **管理角色指派**  *管理角色指派*是管理角色和角色指派原則之間的連結。將管理角色指派給角色指派原則授與能夠使用的 cmdlet 與管理角色中所定義的參數。當您建立角色指派的角色指派原則和管理角色之間時，您無法指定任何範圍。工作分派所套用的範圍為基礎的管理角色及`Self`或`MyGAL`。如需詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

  - **管理角色**  *管理角色*是管理角色項目之群組的容器。角色可用來定義使用者可以運用其信箱或通訊群組的特定工作。*管理角色項目*是 cmdlet、 指令碼或讓每個要執行的管理角色中的特定工作的特殊權限。您只可以使用一般使用者管理角色與角色指派原則。如需詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

  - **管理角色項目**  管理角色項目是在管理角色決定何種 cmdlets 及參數可用來管理角色和角色群組的個別項目。每個角色項目包含單一指令程式和可以存取管理角色的參數。

下圖顯示上述清單中的每個角色指派原則層，以及每個層如何與其他層相關。

**管理角色指派原則模型**

![角色指派模型關係](images/Dd638100.7f7c11ca-0d61-464d-98a3-a9991ec811b5(EXCHG.150).jpg "角色指派模型關係")

如需管理角色、角色指派和範圍的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 預設和明確角色指派原則

下列各節說明 Exchange 2013 中兩種類型的角色指派原則。

## 預設角色指派原則

預設角色指派原則是在信箱建立或移至執行 Exchange 2013 之伺服器時指派給信箱，且角色指派原則不是使用 **New-Mailbox** 或 **Enable-Mailbox** Cmdlet 上的 *RoleAssignmentPolicy* 參數來提供。

Exchange 2013包括提供最常用的權限的使用者預設角色指派原則。您可以新增或移除管理角色或從其變更上預設角色指派原則的預設權限。

如果您想要取代您自己的預設角色指派原則的內建的預設角色指派原則時，您可以使用**Set-RoleAssignmentPolicy**指令程式以選取新的預設值。當您這麼做時，任何新信箱指派所指定之角色指派原則預設如果您沒有明確地指定角色指派原則。

當您變更預設角色指派原則時、 指派預設角色指派原則的信箱不自動指派新的預設角色指派原則。如果您要使用已設定為預設角色指派原則要更新先前建立的信箱，您必須使用**Set-Mailbox**指令程式來達成。

## 明確角色指派原則

明確角色指派原則是您指派給信箱的**New-Mailbox**、 **Set-Mailbox**或**Enable-Mailbox**指令程式使用手動*RoleAssignmentPolicy*參數的原則。當您指定的明確角色指派原則時，新的原則會立即生效和取代先前指派的明確角色指派原則。

## 使用角色指派原則

角色指派原則啟用您量身訂作何種商務為基礎的權限需要您的使用者必須能夠設定。如果預設角色指派原則符合您的需求，您不需要執行任何自訂。不過，如果您有許多不同的使用者群組具有特殊需要，您可以建立角色指派原則的每個。

您使用的預設角色指派原則應包含套用至您最大一組使用者的權限。然後，每個特殊的使用者群組建立角色指派原則並依此修改其增加或減少嚴格的權限授與這些角色指派原則。當您組織在角色指派原則如此一來時，您減少複雜性僅明確雖然大部分的使用者會收到更為常見提供預設角色指派原則的權限指派給特定使用者的角色指派原則。

信箱可以有一個角色指派原則。所有使用者，包括系統管理員和專家使用者都指派一個角色指派原則。如果您想要有一組不同的權限的使用者，您必須在具有必要權限的其他角色指派原則時指派該使用者的信箱。

## 角色指派原則管理

若要新增新的角色指派原則、 您先建立 web 應用程式並決定是否要預設角色指派原則。建立角色指派原則之後，您將管理角色指派給角色指派原則，並再將角色指派原則指派給信箱。您可以稍後選擇新增或移除管理角色或選擇不同的角色指派原則設為預設值。

下表列出角色指派原則層以及您可用於管理每一層的程序主題。

### 角色指派原則管理主題

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>角色指派原則模型層</th>
<th>管理主題</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>信箱</p></td>
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">管理使用者信箱</a></p>
<p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">變更在信箱上的指派原則</a></p></td>
</tr>
<tr class="even">
<td><p>角色指派原則</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色指派原則</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>管理角色及指派</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色指派原則</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>管理角色項目</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">將角色項目新增至角色</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">變更的角色項目</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">從角色移除角色項目</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>變更管理角色的角色指派原則中的管理角色項目是進階的任務以及通常不需要在大多數情況下。您可能會，而能夠使用已經存在的管理角色符合您需求。如需詳細資訊，請參閱<a href="built-in-role-groups-exchange-2013-help.md">內建角色群組</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>

