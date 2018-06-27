---
title: '將角色項目新增至未限定範圍的頂層角色: Exchange 2013 Help'
TOCTitle: 將角色項目新增至未限定範圍的頂層角色
ms:assetid: 52fd3f20-c348-49d5-9bdb-f2cbf780cf2d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd979789(v=EXCHG.150)
ms:contentKeyID: 50473111
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將角色項目新增至未限定範圍的頂層角色

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

您可以新增指令碼和非Exchange指令程式未限定範圍的頂層管理角色如果您想要讓新的指令碼或非Exchange指令程式可以使用現有的未限定範圍角色。這些指令碼和非Exchange cmdlet 會新增為管理角色項目未限定範圍的頂層管理角色。然後可以使用這些未限定範圍的頂層角色項目或任何未限定範圍的角色衍生自最上層角色。如需未限定範圍的角色項目的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要變更包含 Exchange Cmdlet 之管理角色上的角色項目，請參閱<a href="change-a-role-entry-exchange-2013-help.md">變更的角色項目</a>。</td>
</tr>
</tbody>
</table>


要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理角色」項目。

  - 您必須使用命令介面來執行這些程序。

  - 能夠加入的角色項目未限定範圍的最上層角色上預設不包含任何管理角色群組中。您先將未限定範圍角色管理角色給使用者或萬用安全性群組 (USG) 或角色群組指派的使用者即成員使用者是否能夠新增未限定範圍的頂層角色項目之前。如需將角色新增至角色群組、 使用者或 USG 的詳細資訊，請參閱下列主題：
    
      - [管理角色群組](manage-role-groups-exchange-2013-help.md)
    
      - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

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

## 新增指令碼角色項目到未限定範圍的頂層角色

如果您想要將指令碼新增至現有的未限定範圍角色，使用此程序。如果您想要將非Exchange指令程式新增至現有的未限定範圍角色，請參閱本主題稍後的 「 未限定範圍的最上層角色新增非 Exchange cmdlet 角色項目 」。

若要將 Windows PowerShell 指令碼新增至未限定範圍的頂層角色，您必須為該角色新增管理角色項目。角色項目包含您要提供給該角色使用之指令碼的名稱及指令碼的參數。

指令碼必須位於執行Exchange 2013其中使用者可能連接至執行指令碼每台伺服器上的 Microsoft Exchange Server 2013安裝路徑中的指令碼目錄。如果使用者存取執行指令碼，但指令碼不位於使用者連線至Exchange 2013伺服器上，會發生錯誤。根據預設，指令碼目錄路徑為 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts。

將指令碼複製至適當的 Exchange 2013 伺服器並決定要使用的指令碼參數後，可使用下列語法建立角色項目。

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

此範例會將 BulkProvisionUsers.ps1 指令碼以及 *Name* 和 *Location* 參數新增至 IT Scripts 角色。

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Add-ManagementRoleEntry</strong> Cmdlet 會執行基本驗證，以確定您只新增指令碼中存在的參數。不過，在新增角色項目後不會進行進一步的驗證。如果稍後新增或移除參數，您必須手動更新包含指令碼的角色項目。</td>
</tr>
</tbody>
</table>


## 新增非 Exchange Cmdlet 角色項目到未限定範圍的頂層角色

如果您想要新增至現有的未限定範圍角色非Exchange指令程式，使用此程序。如果您想要將指令碼新增至現有的未限定範圍角色，請參閱本主題前面的"新增至未限定範圍的頂層角色的指令碼角色項目 」。

若要將非 Exchange Cmdlet 新增至未限定範圍的頂層角色，您必須為該角色新增管理角色項目。角色項目包含您要提供給該角色使用的 Cmdlet 嵌入式管理單元、Cmdlet 名稱及 Cmdlet 的參數。

如果您將非 Exchange Cmdlet 新增至新角色，Cmdlet 必須安裝在每部 Exchange 2013 伺服器上，而使用者可能連線至此處以執行 Cmdlet。若要了解如何正確安裝與註冊包含您想要使用之 Cmdlet 的 Windows PowerShell 嵌入式管理單元，請參閱產品的說明文件。

在您於適當的 Windows 伺服器上安裝包含 Cmdlet 的 Exchange 2013 PowerShell 嵌入式管理單元，並決定應使用哪些 Cmdlet 參數之後，可使用以下語法建立角色項目。

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

此範例會將 Contoso.Admin.Cmdlets 嵌入式管理單元中的 **Set-WidgetConfiguration** Cmdlet 以及 *Database* 和 *Size* 參數新增至 Widget Cmdlets 角色。

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Add-ManagementRoleEntry</strong> Cmdlet 會執行基本驗證，以確定您只新增 Cmdlet 中存在的參數。不過，在新增角色項目後不會進行進一步的驗證。如果稍後變更 Cmdlet 並新增或移除參數，您必須手動更新包含 Cmdlet 的角色項目。</td>
</tr>
</tbody>
</table>


## 其他工作

在您新增角色項目或未限定範圍的頂層角色之後，您可能還想要：

[將角色項目新增至角色](add-a-role-entry-to-a-role-exchange-2013-help.md)

[管理角色群組](manage-role-groups-exchange-2013-help.md)

[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)

[將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[移除使用者或 USG 的角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

