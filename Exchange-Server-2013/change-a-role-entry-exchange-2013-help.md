---
title: '變更的角色項目: Exchange 2013 Help'
TOCTitle: 變更的角色項目
ms:assetid: 5aa4f39c-16a4-4815-ac4f-2cdcfa2b3ee1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298005(v=EXCHG.150)
ms:contentKeyID: 50473227
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 變更的角色項目

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

管理角色每個管理角色項目代表單一指令程式。將參數加入至或來自會新增至管理角色、 角色項目移除參數來控制這些參數是否可在該指令程式。如需管理角色項目在 Microsoft Exchange Server 2013的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

您無法修改內建管理角色上的角色項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題不會討論如何修改未限定範圍的管理角色上未限定範圍的管理角色項目。如需如何修改未限定範圍的角色項目的詳細資訊，請參閱<a href="create-a-role-exchange-2013-help.md">建立角色</a>。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要新增或移除角色項目中的參數，您必須使用<em>AddParameter</em>或<em>RemoveParameter</em>參數。如果省略了<em>AddParameter</em>或<em>RemoveParameter</em>參數執行<strong>Set-ManagementRoleEntry</strong>指令程式時，僅使用<em>Parameters</em>參數指定的參數將會包含在角色項目。將移除角色項目中的所有其他參數。</td>
</tr>
</tbody>
</table>


要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理角色」項目。

  - 您必須使用命令介面來執行這些程序。

  - 如果您想要將參數新增至角色項目、 新增參數必須存在於父系角色中的角色項目。在您指定此指令程式也必須存在於參數。

  - 如果您想要從角色項目移除參數，您移除的參數不能存在於中的所有子系角色的角色項目。您必須從的子系角色的角色項目移除參數。使用本主題稍後的 「 使用命令介面從角色項目中移除一或多個參數 」 程序中的所有子系角色的角色項目移除參數。

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

若要新增的角色項目參數，您需要指定您想要新增使用*Parameters*參數的參數。然後您需要指定*AddParameter*參數，以指出想要執行 「 新增 」 作業。

若要將參數新增至角色項目，請使用下列語法。

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter

此範例會新增 *EmailAddresses* 和 *Type* 參數到收件者系統管理員角色上的 **Set-Mailbox** Cmdlet。

    Set-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" -Parameters EmailAddresses, Type -AddParameter

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351162\(v=exchg.150\))。

## 使用命令介面從角色項目移除一或多個參數

若要從角色項目移除參數，您需要指定您想要移除*Parameters*參數的參數。然後您需要指定*RemoveParameter*參數，以指出想要執行的移除作業。

若要從角色項目移除參數，請使用下列語法。

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter

此範例會從 Tier 1 伺服器系統管理員角色上的 **Set-SendConnector** Cmdlet 移除 *Port*、*ProtocolLoggingLevel* 和 *SmartHostAuthMechanism* 參數。

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Set-SendConnector" -Parameters Port, ProtocolLoggingLevel, SmartHostAuthMechanism -RemoveParameter

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351162\(v=exchg.150\))。

## 使用命令介面從角色項目移除所有參數

若要從角色項目移除所有的參數，您需要在*Parameters*參數指定值`$Null` 。您不需要加上*RemoveParameters*參數。

從角色項目移除所有參數時最適合您想要在指令程式提供只有幾個參數清單與排除的所有其他參數。如果您不想的角色存取權給指令程式，移除完全而不是只移除參數的角色相關聯的角色項目。如需如何從角色移除角色項目，請參閱[從角色移除角色項目](remove-a-role-entry-from-a-role-exchange-2013-help.md)的詳細資訊。

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

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters $Null 

此範例會從收件者系統管理員角色的 **Set-CASMailbox** Cmdlet 上移除所有參數。

    Set-ManagementRoleEntry "Recipient Administrators\Set-CASMailbox" -Parameters $Null 

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351162\(v=exchg.150\))。

## 使用命令介面來套用特定的一組參數

如果您想只有一組特定的角色項目中要包含的參數，指定*Parameters*參數僅。不包含*AddParameter*或*RemoveParameter*參數。當您指定只*Parameters*參數時，只有在命令中指定的參數隨附在角色項目。會移除所有其他參數。

若要指定特定的一組參數，請使用下列語法。

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

此範例會在 Seattle 郵件收件者角色的 **Set-UMMailbox** Cmdlet 上只包含 *Identity*、*DisplayName*、*MissedCallNotificationEnabled* 和 *PersonalAuthAttendantEnabled* 參數。

    Set-ManagementRoleEntry "Seattle Mail Recipients\Set-UMMailbox" -Parameters Identity, DisplayName, MissedCallNotificationEnabled, PersonalAutoAttendantEnabled

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd351162\(v=exchg.150\))。

