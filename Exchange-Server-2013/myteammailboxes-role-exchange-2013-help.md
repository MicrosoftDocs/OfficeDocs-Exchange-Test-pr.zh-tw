---
title: 'MyTeamMailboxes 角色: Exchange 2013 Help'
TOCTitle: MyTeamMailboxes 角色
ms:assetid: 269bf64a-5028-40e4-96ec-17c362a73e69
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673048(v=EXCHG.150)
ms:contentKeyID: 50472859
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# MyTeamMailboxes 角色

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

`MyTeamMailboxes` 管理角色讓個別使用者可建立站台信箱並連線至 Microsoft SharePoint 網站。

此管理角色是 Microsoft Exchange Server 2013 中，角色型存取控制 (RBAC) 權限模型的其中一個內建角色。指派給一或多個管理角色群組、管理角色指派原則、使用者或萬用資訊安全群組 (USG) 的管理角色，會作為 Cmdlet 或指令碼的邏輯群組，合併後可提供檢視或修改 Exchange 2013 元件 (例如信箱資料庫、傳輸規則和收件者) 組態的存取權。如果 Cmdlet 或指令碼及其參數 (合稱管理角色項目) 包含在角色中，則該 Cmdlet 或指令碼及其參數可以由指派的角色執行。如需管理角色和管理角色項目的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

如需管理角色、管理角色群組和其他 RBAC 元件的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 管理角色指派

若要讓此角色授予權限，即必須將角色指派給角色受託人，像是角色指派原則。這項指派是運用管理角色指派完成。角色指派會連結角色受託人與角色。如果指派多個角色給一個角色受託人，則會授與角色受託人所指派全部角色授與的所有權限組合。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以將此管理角色指派給角色群組、USG，或直接指派給使用者。但是，以使用者為主的角色與角色指派原則搭配使用時最有效。</td>
</tr>
</tbody>
</table>


這個以使用者為主的角色有隱含的範圍，不能修改。因此，您不應將自訂的範圍新增至將此角色指派給角色指派原則、角色群組、USG 或使用者的角色指派。

如需角色指派和範圍的詳細資訊，請參閱下列主題：

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

根據預設，此角色會指派給一或多個角色指派原則。如需相關資訊，請參閱＜預設管理角色指派＞一節。

如果您要檢視指派給此角色的角色群組、使用者或 USG 的清單，請使用下列命令。

    Get-ManagementRoleAssignment -Role "<role name>"

## 一般和委派角色指派

可以使用一般或委派角色指派將此角色指派給角色受託人。一般角色指派會將角色提供的權限授與角色受託人。委派角色指派則會授與角色受託人，將角色指派給其他角色受託人的能力。如需一般和委派角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

## 新增或移除角色指派

您可以變更獲指派這個角色的角色受託人。變更指派有此角色的角色受託人，就可以變更獲授予其權限的人。您可以將此角色指派給其他內建角色指派原則，或者建立角色指派原則，並將此角色指派給這些指派原則。

若要將此角色指派給角色受託人，必須使用委派角色指派，將角色指派給您所屬的角色群組、直接指派給您，或是您所屬的 USG。如需委派角色指派的詳細資訊，請參閱＜一般和委派角色指派＞一節。

您也可以將此角色從預設角色指派原則、您所建立的角色指派原則和角色群組、使用者和 USG 中移除。不過，此角色與角色群組或 USG 之間，至少一定要有一個委派角色指派。您無法刪除最後一個委派角色指派。

如需如何在此角色與角色群組、使用者和 USG 之間新增或移除指派的詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的「新增角色至角色群組或移除其中的角色」一節

  - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [移除使用者或 USG 的角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## 啟用或停用角色指派

透過啟用或停用角色指派，即可控制該角色指派是否應生效。如果停用角色指派，則相關聯角色授與的權限不會套用至角色受託人。如此可方便您暫時移除權限，而不刪除角色指派。如需詳細資訊，請參閱[變更角色指派](change-a-role-assignment-exchange-2013-help.md)。

## 預設管理角色指派

這個角色具有一或多個角色受託人的角色指派。下表指出角色指派為一般或委派，同時指出套用至每個指派的管理範圍。下列清單說明每個資料行：

  - **一般指派**   一般角色指派可讓角色受託人存取此角色上的管理角色項目提供的權限。

  - **委派指派**   委派角色指派可讓角色受託人將此角色指派給角色群組、使用者或 USG。

  - **收件者讀取範圍**   收件者讀取範圍決定角色受託人可從 Active Directory 讀取的收件者物件。

  - **收件者寫入範圍**   收件者寫入範圍決定角色受託人可在 Active Directory 中修改的收件者物件。

  - **組態讀取範圍**   組態讀取範圍決定角色受託人可從 Active Directory 讀取的組態和伺服器物件。

  - **組態寫入範圍**   組態寫入範圍決定角色受託人可在 Active Directory 中修改的組態和伺服器物件。

### 此角色的預設管理角色指派

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
<th>角色群組或指派原則</th>
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
<td><p>預設角色指派原則。</p>
<p>如需相關資訊，請參閱<a href="understanding-management-role-assignment-policies-exchange-2013-help.md">了解管理角色指派原則</a>。</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## 管理角色自訂

此角色已設定為對角色受託人提供所有必要的 Cmdlet 及參數，以便管理本主題開頭所列的功能和元件。另外也已提供其他角色，以便管理其他功能。透過在角色群組中新增和移除角色，您就可以建立自訂的權限模型，而不需要自訂個別管理角色。如需完整的角色清單，請參閱 [內建管理角色](built-in-management-roles-exchange-2013-help.md)。如需自訂角色群組的詳細資訊，請參閱 [管理角色群組](manage-role-groups-exchange-2013-help.md)。

如果您決定要建立此角色的自訂版本，則必須建立此角色的子角色，然後自訂這個新角色。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>以下資訊可讓您執行進階的權限管理。自訂管理角色可能會大幅增加權限模型的複雜度。如果您以設定不正確的自訂角色取代內建管理角色，可能導致某些功能停止運作。</td>
</tr>
</tbody>
</table>


以下是建立自訂角色並將其指派給角色受託人時最常用的步驟：

1.  建立此角色的複本。如需詳細資訊，請參閱[建立角色](create-a-role-exchange-2013-help.md)。

2.  使用 **Set-ManagementRoleEntry** 和 **Remove-ManagementRoleEntry** Cmdlet 變更或移除新角色上的角色項目。您無法新增其他角色項目至新角色，因爲新角色只能包含內建上層角色上的角色項目。如需相關資訊，請參閱下列主題：
    
      - [變更的角色項目](change-a-role-entry-exchange-2013-help.md)
    
      - [從角色移除角色項目](remove-a-role-entry-from-a-role-exchange-2013-help.md)

3.  如果您要以此自訂的新角色取代內建角色，請移除與內建角色相關聯的任何角色指派。如需相關資訊，請參閱下列主題：
    
      - [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的「新增角色至角色群組或移除其中的角色」一節
    
      - [移除使用者或 USG 的角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

4.  將自訂的新角色新增至所需的角色受託人。如需相關資訊，請參閱下列主題：
    
      - [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的「新增角色至角色群組或移除其中的角色」一節
    
      - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果除了建立角色的使用者以外，您要讓其他使用者也能指派新的自訂角色，務必將「委派角色指派」的權限新增到至少一位角色受託人。如需詳細資訊，請參閱<a href="delegate-role-assignments-exchange-2013-help.md">委派角色指派</a>。</td>
        </tr>
        </tbody>
        </table>

