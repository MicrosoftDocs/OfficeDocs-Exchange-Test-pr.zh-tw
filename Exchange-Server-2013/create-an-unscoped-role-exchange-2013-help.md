---
title: '建立未限定範圍的角色: Exchange 2013 Help'
TOCTitle: 建立未限定範圍的角色
ms:assetid: 5a042ccf-4d5f-4609-a91b-21c20d1e6459
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876886(v=EXCHG.150)
ms:contentKeyID: 50473205
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立未限定範圍的角色

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-06-09_

未限定範圍的管理角色可以用來為系統管理員和專家使用者提供 Windows PowerShell 指令碼和非 Exchange Cmdlet 的存取權。您可以建立未限定範圍的頂層角色，並將指令碼或非 Exchange Cmdlet 新增到該角色，或根據現有未限定範圍的頂層角色來建立角色。在建立和自訂未限定範圍的角色之後，可以將角色指派給管理角色群組、使用者和萬用安全性群組 (USG)。未限定範圍的角色不能指派給管理角色指派原則。如需未限定範圍的角色的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>顧名思義，未限定範圍的角色不需套用管理範圍，因此其權利是很強大的。這表示該角色可以針對 Exchange 組織中的任何物件執行其所包含的指令碼和非 Exchange Cmdlet。當新增指令碼或非 Exchange Cmdlet 到未限定範圍的角色時，以及指派未限定範圍的角色時，可考慮到這點。</td>
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
<td>如果您要建立包含 Exchange Cmdlet 的角色，則必須根據現有的管理角色來建立角色。如需建立包含 Exchange Cmdlet 的角色的詳細資訊，請參閱<a href="create-a-role-exchange-2013-help.md">建立角色</a>。</td>
</tr>
</tbody>
</table>


要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理角色」項目。

  - 您必須使用命令介面來執行這些程序。

  - 根據預設，不會在任何管理角色群組中包含建立未限定範圍之角色的能力。您必須先將未限定範圍的角色管理角色指派給使用者，或指派給 USG 或成員為使用者的角色群組，使用者才能够建立角色群組。如需將角色新增至使用者、USG 或角色群組的詳細資訊，請參閱下列主題：
    
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

## 建立未限定範圍的頂層管理角色

如果要在組織中建立可讓系統管理員或專家使用的指令碼或非 Exchange Cmdlet，您需要建立未限定範圍的頂層角色。因爲不會從其他角色繼承初始之未限定範圍的角色，所以指令碼和非 Exchange Cmdlet 只能新增到建立為頂層角色的未限定範圍角色。然後，新的未限定範圍頂層角色就可以成為其他未限定範圍角色的上層，這些角色也可以使用新增的指令碼和非 Exchange Cmdlet。

建立未限定範圍之頂層角色的步驟如下：

## 步驟 1：建立未限定範圍的頂層角色

未限定範圍的頂層角色沒有上層角色。您需要指定 *UnscopedTopLevel* 參數來建立沒有上層的角色。使用下列語法建立新角色。

    New-ManagementRole <name of new role> -UnscopedTopLevel

此範例會建立 IT 指令碼未限定範圍的頂層角色。

    New-ManagementRole "IT Scripts" -UnscopedTopLevel

建立角色之後，在新增指令碼或非 Exchange Cmdlet 給角色之前，角色都是空的。

如需詳細的語法及參數資訊，請參閱 [New-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd298073\(v=exchg.150\))。

## 步驟 2a：新增指令碼管理角色項目

如果您要新增指令碼到新的未限定範圍角色，請使用此步驟。如果您要新增非 Exchange Cmdlet 到新的未限定範圍角色，請使用Step 2b。

若要將 Windows PowerShell 指令碼新增至未限定範圍的頂層角色，您必須為該角色新增管理角色項目。角色項目包含您要提供給該角色使用之指令碼的名稱及指令碼的參數。

在使用者可能連線以執行指令碼的每一部執行 Exchange 2013 的伺服器上，指令碼必須位於 Microsoft Exchange Server 2013 安裝路徑的 `RemoteScripts` 目錄中。如果使用者擁有執行指令碼的存取權，但指令碼不是位於使用者連接的 Exchange 2013 伺服器上，就會發生錯誤。根據預設，`RemoteScripts` 目錄的路徑為 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts。

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


## 步驟 2b：新增非 Exchange Cmdlet 角色項目

如果您要新增非 Exchange Cmdlet 到新的未限定範圍角色，請使用此步驟。如果您要新增指令碼到新的未限定範圍角色，請使用Step 2a。

若要將非 Exchange Cmdlet 新增至未限定範圍的頂層角色，您必須為該角色新增管理角色項目。角色項目包含您要提供給該角色使用的 Cmdlet 嵌入式管理單元、Cmdlet 名稱及 Cmdlet 的參數。

如果您將非 Exchange Cmdlet 新增至新角色，Cmdlet 必須安裝在每部 Exchange 2013 伺服器上，而使用者可能連線至此處以執行 Cmdlet。若要了解如何正確安裝與註冊包含您想要使用之 Cmdlet 的 Windows PowerShell 嵌入式管理單元，請參閱產品的說明文件。

在您於適當的 Windows 伺服器上安裝包含 Cmdlet 的 Exchange 2013 PowerShell 嵌入式管理單元，並決定應該使用哪些 Cmdlet 參數之後，可使用以下語法建立角色項目。

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


## 步驟 3：指派管理角色

建立與設定角色的最後一個步驟是將其指派給角色受託人。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>無法在指派未限定範圍之角色的角色指派上設定管理範圍。不論您選擇的是為角色群組、使用者還是 USG 建立角色指派，您都必須選擇建立不含管理範圍之角色指派的選項。</td>
</tr>
</tbody>
</table>


您可以將新角色指派給角色群組、使用者或 USG。如需詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

## 以另一個未限定範圍角色為基礎建立未限定範圍的角色

如果您有現存未限定範圍的頂層角色，或其他為新未限定範圍角色之基礎的未限定範圍角色，您就可以建立下層的未限定範圍角色。下層的未限定範圍角色可以包含存在於上層未限定範圍角色的指令碼和 Cmdlet 的子集。例如，如果您只提供可在上層未限定範圍角色上使用的指令碼或 Cmdlet 的子集給經驗不足的系統管理員，這方法便非常實用。

建立未限定範圍之下層角色的步驟如下：

## 步驟 1：建立未限定範圍的下層角色

新的未限定範圍之下層角色可以現有的未限定範圍角色為基礎。建立角色時，會將現有的角色及其管理角色項目複製到新的角色。現有的角色會成為新下層角色的父項。如果您根據另一個未限定範圍的角色建立未限定範圍的角色，則必須選擇包含所有 Cmdlet 的角色，以及需要使用的參數，然後再移除不要的項目。未限定範圍的下層角色不可擁有不存在於上層角色的管理角色項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您需要建立包含不存在於任何其他未限定範圍角色中的指令碼或非 Exchange Cmdlet 的未限定範圍角色，請建立未限定範圍的頂層角色。如需詳細資訊，請參閱本主題稍早的Create an unscoped top-level management role。</td>
</tr>
</tbody>
</table>


使用下列語法建立新角色。

    New-ManagementRole -Parent <existing unscoped role to copy> -Name <name of new unscoped role>

此範例會將 IT 全域指令碼角色及其管理角色項目複製到診斷 IT 指令碼角色。

    New-ManagementRole -Parent "IT Global Scripts" -Name "Diagnostic IT Scripts"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd298073\(v=exchg.150\))。

## 步驟 2：變更角色的管理角色項目

建立角色後，您需要變更角色的項目。您可以移除整個角色項目，此項目會完全移除對關聯指令碼或非 Exchange Cmdlet 的存取。或者，您可以從角色項目移除參數，以便移除關聯之指令碼或非 Exchange Cmdlet 上的那些特定參數的存取權。

您無法在角色項目上新增角色項目或參數，除非它們存在於上層角色中。因為您剛剛才在步驟 1 中從上層角色建立角色，因此無法在角色項目上新增任何其他的角色項目或參數，因為其不存在於上層角色中。

在變更角色的角色項目時，可以進行下列其中一項動作：

  - 移除單一、整個角色項目。

  - 移除多個、整個角色項目。

  - 從角色項目移除參數。

若要從新角色移除角色項目，請參閱[從角色移除角色項目](remove-a-role-entry-from-a-role-exchange-2013-help.md)。

## 步驟 3：指派管理角色

建立與設定角色的最後一個步驟是將其指派給角色指派者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>無法在指派未限定範圍之角色的角色指派上設定管理範圍。不論您選擇的是為角色群組、使用者還是 USG 建立角色指派，您都必須選擇建立不含管理範圍之角色指派的選項。</td>
</tr>
</tbody>
</table>


您可以將新角色指派給角色群組、使用者或 USG。如需相關資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

