---
title: '變更未限定範圍的頂層角色的角色項目: Exchange 2013 Help'
TOCTitle: 變更未限定範圍的頂層角色的角色項目
ms:assetid: 65c0bfb3-aafd-4c64-8429-7616c57adf1c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876896(v=EXCHG.150)
ms:contentKeyID: 50473361
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 變更未限定範圍的頂層角色的角色項目

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

在未限定範圍的頂層管理角色的管理角色項目，請參閱指令碼和非Exchange cmdlet 以及您想要提供給這些指派角色及其參數。變更的角色項目上可用的參數，您控制哪些那些指派角色可以執行指令碼或非Exchange指令程式。如需未限定範圍的角色項目的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

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

  - 能夠變更未限定範圍的頂層角色的角色項目不是預設包括於任何管理角色群組中。您先將未限定範圍角色管理角色給使用者或萬用安全性群組 (USG) 指派或角色群組的使用者為其成員，才能使用者是否能夠新增或變更的未限定範圍的頂層角色項目。如需將角色新增至使用者、 USG 或角色群組的詳細資訊，請參閱下列主題：
    
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

## 使用命令介面將一或多個參數新增至角色項目

若要新增未限定範圍的頂層角色項目參數，您需要執行下列動作：

  - 指定您想要新增使用*Parameters*參數的參數。

  - 指定*AddParameter*參數以指出想要執行 「 新增 」 作業。

  - 指定*UnscopedTopLevel*參數表示您要變更未限定範圍的頂層角色的角色項目。如果您未指定此參數變更未限定範圍角色的角色項目時，會發生錯誤。

若要將參數新增至角色項目，請使用下列語法。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter -UnscopedTopLevel

本範例會新增至收件者系統管理員未限定範圍角色上**CreateUsers.ps1**指令碼*EmailAddress*與*City*參數。

    Set-ManagementRoleEntry "Recipient Administrators\CreateUsers.ps1" -Parameters EmailAddress, City -AddParameter -UnscopedTopLevel

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351162\(v=exchg.150\))。

## 使用命令介面從角色項目移除一或多個參數

若要從角色項目移除參數，您需要執行下列動作：

  - 指定您想要移除*Parameters*參數的參數。

  - 指定*RemoveParameter*參數以指出想要執行的移除作業。

  - 指定*UnscopedTopLevel*參數表示您要變更未限定範圍的頂層角色的角色項目。如果您未指定此參數變更未限定範圍角色的角色項目時，會發生錯誤。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法復原移除作業。如果您遭移除的角色項目參數，則必須再次手動新增。</td>
</tr>
</tbody>
</table>


若要從角色項目移除參數，請使用下列語法。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter -UnscopedTopLevel

此範例會將*Delay*、 *Force*，以及*Credential*參數移除**Start-Widget**非Exchange指令程式上的層 1 伺服器管理員角色。

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Start-Widget" -Parameters Delay, Force, Credential -RemoveParameter -UnscopedTopLevel

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351162\(v=exchg.150\))。

## 使用命令介面從角色項目移除所有參數

若要從角色項目中移除所有的參數，您需要執行下列動作：

  - 在*Parameters*參數指定值`$Null` 。您不需要加上*RemoveParameter*參數。

  - 指定*UnscopedTopLevel*參數表示您要變更未限定範圍的頂層角色的角色項目。如果您未指定此參數變更未限定範圍角色的角色項目時，會發生錯誤。

從角色項目移除所有參數時最適合您想要讓只有幾個參數可在指令碼或非Exchange指令程式清單與排除的所有其他參數。

如果您不想讓指令碼或非Exchange指令程式的存取權的角色，移除完全而不是只移除參數的角色相關聯的角色項目。如需如何從角色移除角色項目，請參閱[從角色移除角色項目](remove-a-role-entry-from-a-role-exchange-2013-help.md)的詳細資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法復原移除作業。如果您遭移除角色項目的所有參數，則必須再次手動新增。</td>
</tr>
</tbody>
</table>


若要從角色項目移除所有參數，請使用下列語法。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters $Null -UnscopedTopLevel

此範例會移除 FindMailboxesOverQuota.ps1 指令碼上的收件者系統管理員角色中的所有參數。

    Set-ManagementRoleEntry "Recipient Administrators\FindMailboxesOverQuota.ps1" -Parameters $Null -UnscopedTopLevel

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351162\(v=exchg.150\))。

## 使用命令介面來套用特定的一組參數

如果您想只有一組特定的角色項目中要包含的參數，您需要執行下列動作：

  - 指定只*Parameters*參數。不包含*AddParameter*或*RemoveParameter*參數。

  - 指定*UnscopedTopLevel*參數表示您要變更未限定範圍角色的角色項目。如果您未指定此參數變更未限定範圍的頂層角色的角色項目時，會發生錯誤。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您指定只<em>Parameters</em>參數時，只有在命令中指定的參數隨附在角色項目。會移除所有其他參數。</td>
</tr>
</tbody>
</table>


若要指定特定的一組參數，請使用下列語法。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -UnscopedTopLevel

本範例會包含只*Alias*、 *DisplayName*、 *WidgetConfig*、 及 「 西雅圖信箱收件者系統管理員 」 角色上**Set-Widget**指令程式上的*Enabled*參數。

    Set-ManagementRoleEntry "Seattle Mail Recipient Admins\Set-UMMailbox" -Parameters Alias, DisplayName, WidgetConfig, Enabled -UnscopedTopLevel

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351162\(v=exchg.150\))。

## 其他工作

變更未限定範圍的頂層角色的角色項目之後，您可能也想要：

[將角色項目新增至角色](add-a-role-entry-to-a-role-exchange-2013-help.md)

[管理角色群組](manage-role-groups-exchange-2013-help.md)

[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)

[將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[移除使用者或 USG 的角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

