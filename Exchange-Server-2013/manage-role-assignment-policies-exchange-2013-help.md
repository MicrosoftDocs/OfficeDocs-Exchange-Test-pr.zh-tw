---
title: '管理角色指派原則: Exchange 2013 Help'
TOCTitle: 管理角色指派原則
ms:assetid: f93d502e-5df4-4ba0-b68d-01a17ccffb4d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657511(v=EXCHG.150)
ms:contentKeyID: 50474640
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理角色指派原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-09_

如果您想要自訂的權限指派給一群使用者，建立新的自訂管理角色指派原則。指派原則您建立可自訂以符合使用者的特定需求。如需 Microsoft Exchange Server 2013中指派原則的詳細資訊，請參閱[了解管理角色指派原則](understanding-management-role-assignment-policies-exchange-2013-help.md)。

要尋找與管理的權限相關的其他管理工作嗎？取出[權限](permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「指派原則」項目。

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

## 新增指派原則

您已建立新的指派原則之後，您將使用者指派給它。如需詳細資訊，請參閱[變更在信箱上的指派原則](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)。

## 使用 EAC 建立新的指派原則

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只能建立使用 Exchange 系統管理中心 (EAC) 的明確指派原則。如果您想要建立新的預設指派原則時，您必須使用Exchange管理命令介面。如需詳細資訊，請參閱本主題稍後的 「 使用命令介面建立預設指派原則 」 一節。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中導覽至 \[權限\] \> \[使用者角色\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在角色指派原則視窗中，提供新指派原則的名稱。

3.  選取核取方塊旁的角色或您想要新增至指派原則的角色。您可以選取多個角色，包括已新增的使用者角色。如果您選取具有子系角色的角色，會自動選取子系角色。

4.  按一下 \[儲存\]，以將變更儲存到指派原則。

## 使用命令介面來建立明確指派原則

若要建立可手動指派至信箱的明確指派原則，請使用下列語法。

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign>

這個範例會建立明確指派原則「限制的信箱組態」，並對它指派 `MyBaseOptions`、`MyAddressInformation` 和 `MyDisplayName` 角色。

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName

如需詳細的語法及參數資訊，請參閱 [New-RoleAssignmentPolicy](https://technet.microsoft.com/zh-tw/library/dd638101\(v=exchg.150\))。

## 使用命令介面來建立預設指派原則

若要建立可指派至新信箱的預設指派原則，請使用下列語法。

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign> -IsDefault

這個範例會建立預設指派原則「限制的信箱組態」，並對它指派 `MyBaseOptions`、`MyAddressInformation` 和 `MyDisplayName` 角色。

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName -IsDefault

如需詳細的語法及參數資訊，請參閱 [New-RoleAssignmentPolicy](https://technet.microsoft.com/zh-tw/library/dd638101\(v=exchg.150\))。

## 移除指派原則

如果您不再需要某個管理角色指派原則，可以加以移除。

## 開始之前有哪些須知？

  - 已指派之所有使用者必須都變更為另一個指派原則。如需如何變更在信箱上的指派原則的詳細資訊，請參閱[變更在信箱上的指派原則](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)。

  - 必須移除指派原則和指派的管理角色之間的所有管理角色指派。如需如何移除指派原則的角色指派的詳細資訊，請參閱本主題稍後的 \[使用命令介面來移除角色指派原則\] 區段。

  - 如果您想移除預設指派原則，這個指派原則必須是 Exchange 2013 組織中的最後一個指派原則。

## 使用 EAC 移除指派原則

1.  在 EAC 中，瀏覽至 \[權限\] \> \[使用者角色\]。

2.  選取您要移除的指派原則，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

## 使用命令介面來移除指派原則

若要移除指派原則，請使用下列語法。

    Remove-RoleAssignmentPolicy <role assignment policy>

此範例會移除 New York Temporary Users 指派原則。

    Remove-RoleAssignmentPolicy "New York Temporary Users"

如需詳細的語法及參數資訊，請參閱 [Remove-RoleAssignmentPolicy](https://technet.microsoft.com/zh-tw/library/dd638190\(v=exchg.150\))。

## 檢視指派原則或指派原則詳細資料的清單

視您想要的資訊，以及使用 EAC 或是命令介面而定，您有多種方式可用來檢視管理角色指派原則。

在 EAC 中，您可以檢視指派給他們的角色指派原則的清單。在命令介面中，您可以檢視您組織中所有指派原則、 列出指派特定的原則及其他的信箱。

## 使用 EAC 來檢視指派原則的清單

1.  在 EAC 中，瀏覽至 \[**權限**\>**使用者角色**。所有在組織中的工作分派原則是在這裡列出。

2.  若要檢視特定的指派原則的詳細資訊，請選取您要檢視指派原則。在詳細資料窗格中顯示的描述及指派給指派原則的角色。

## 使用命令介面來檢視指派原則的清單

當您執行 **Get-RoleAssignmentPolicy** Cmdlet 時，透過不指定任何指派原則，可以在組織中檢視所有指派原則的清單。

此程序會使用管線及**Format-Table**指令程式。如需這些概念的詳細資訊，請參閱下列主題：

  - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))

  - [使用命令輸出](working-with-command-output-exchange-2013-help.md)

若要傳回組織中所有指派原則的清單，請使用以下命令。

    Get-RoleAssignmentPolicy

若要傳回組織中的所有工作分派原則的特定屬性的清單，您可以將傳送到**Format-Table** cmdlet 的結果與結果的清單中指定想要的內容。使用下列語法。

    Get-RoleAssignmentPolicy | Format-Table <property 1>, <property 2...>

此範例會傳回組織中所有指派原則的清單，並包含 **Name** 及 **IsDefault** 內容。

    Get-RoleAssignmentPolicy | Format-Table Name, IsDefault

如需詳細的語法及參數資訊，請參閱 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 或 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/zh-tw/library/dd638195\(v=exchg.150\))。

## 使用命令介面來檢視單一指派原則的詳細資料

您也可使用 **Get-RoleAssignmentPolicy** Cmdlet，並以管線將輸出傳送至 **Format-List** Cmdlet，以檢視特定指派原則的詳細資料。

此程序會使用管線及**Format-List**指令程式。如需這些概念的詳細資訊，請參閱下列主題：

  - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))

  - [使用命令輸出](working-with-command-output-exchange-2013-help.md)

若要檢視特定指派原則的詳細資料，請使用下列語法。

    Get-RoleAssignmentPolicy <assignment policy name> | Format-List

此範例會檢視 Redmond 使用者（沒有「簡訊」指派原則）的詳細資料。

    Get-RoleAssignmentPolicy "Redmond Users - no Text Messaging" | Format-List

如需詳細的語法及參數資訊，請參閱 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 或 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/zh-tw/library/dd638195\(v=exchg.150\))。

## 使用命令介面來尋找預設指派原則

您可以透過管線傳送 format-list **Get-RoleAssignmentPolicy**指令程式在**Where** cmdlet 的輸出找到預設指派原則。使用**Where**指令程式篩選顯示只能指派原則已設為`$True`其*IsDefault*屬性傳回的資料。

此程序會使用管線及**Where**指令程式。如需這些概念的詳細資訊，請參閱下列主題：

  - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))

  - [使用命令輸出](working-with-command-output-exchange-2013-help.md)

這個範例會傳回預設的指派原則。

    Get-RoleAssignmentPolicy | Where { $_.IsDefault -eq $True }

如需詳細的語法及參數資訊，請參閱 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 或 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/zh-tw/library/dd638195\(v=exchg.150\))。

## 使用命令介面來檢視有指派特定原則的信箱

您可以找到所有的信箱已指派特定透過管線傳送 format-list **Get-Mailbox**指令程式在**Where** cmdlet 的輸出。使用**Where**指令程式篩選傳回的資料來顯示其*RoleAssignmentPolicy*屬性設定為您指定的指派原則名稱的信箱。

此程序會使用管線及**Where**指令程式。如需這些概念的詳細資訊，請參閱下列主題：

  - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))

  - [使用命令輸出](working-with-command-output-exchange-2013-help.md)

使用下列語法。

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<role assignment policy>" }

此範例會找出所有均指派溫哥華一般使用者原則的信箱。

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Vancouver End Users" }

如需詳細的語法及參數資訊，請參閱 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 或 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/zh-tw/library/dd638195\(v=exchg.150\))。

## 變更預設指派原則

您可以變更指派給新的信箱所建立的管理角色指派原則。變更預設角色指派原則不會變更指派原則指派給現有的信箱。若要變更指派原則指派給現有的信箱，請參閱[變更在信箱上的指派原則](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來變更預設指派原則。您必須使用命令介面。</td>
</tr>
</tbody>
</table>


## 使用命令介面來變更預設的指派原則

若要變更預設的指派原則，請使用下列語法。

    Set-RoleAssignmentPolicy <assignment policy name> -IsDefault

此範例會設定 Vancouver End Users 指派原則作為預設的指派原則。

    Set-RoleAssignmentPolicy "Vancouver End Users" -IsDefault

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>新的信箱即使原則尚未指派管理角色指派預設指派原則。指定與未指派的管理角色指派原則的信箱無法存取任何 Microsoft Outlook Web App 中的信箱設定功能。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Set-RoleAssignmentPolicy](https://technet.microsoft.com/zh-tw/library/dd638090\(v=exchg.150\))。

## 將角色新增至指派原則

## 使用 EAC 將角色新增至指派原則

1.  在 EAC 中，瀏覽至 \[權限\] \> \[使用者角色\]。

2.  選取要新增一個或多個角色的指派原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  選取核取方塊旁的角色或您想要新增至指派原則的角色。您可以選取多個角色，包括已新增的使用者角色。如果您選取具有子系角色的角色，會自動選取子系角色。

4.  按一下 \[儲存\]，以將變更儲存到指派原則。

## 使用命令介面將角色新增至工作指派原則

若要在角色和指派原則之間建立管理角色指派，請使用以下語法。

    New-ManagementRoleAssignment -Name <role assignment name> -Role <role name> -Policy <assignment policy name>

此範例會在 MyVoicemail 角色和 Seattle 使用者指派原則之間建立角色指派 Seattle 使用者 - 語音信箱。

    New-ManagementRoleAssignment -Name "Seattle Users - Voicemail" -Role MyVoicemail -Policy "Seattle Users"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 移除指派原則中的角色

如果您不想讓管理其信箱或通訊群組的特定功能的權限的使用者，您可以移除授與的權限的使用者會被指派管理角色指派原則的管理角色。如果相同的工作分派原則指派給其他使用者，他們也會失去管理該功能的能力。

## 使用 EAC 從指派原則移除角色

1.  在 EAC 中，瀏覽至 \[權限\] \> \[使用者角色\]。

2.  選取您要移除一或多個角色的指派原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  清除您要移除指派原則角色或角色旁的核取方塊。如果清除核取方塊已經子系角色的角色，也會清除子系角色核取方塊。

4.  按一下 \[儲存\]，以將變更儲存到指派原則。

## 使用命令介面從指派原則移除角色

您可以使用 **Get-ManagementRoleAssignment** 指令程式來擷取關聯的管理角色，然後將傳回的角色指派以管線傳輸至 **Remove-ManagementRoleAssignment** 指令程式，即可從指派原則移除角色。

如需一般和委派角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

此程序會使用管線。如需以管線傳送的詳細資訊，請參閱[管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))。

若要從指派原則移除角色，請使用下列語法。

    Get-ManagementRoleAssignment -RoleAssignee <assignment policy name> -Role <role name> | Remove-ManagementRoleAssignment

這個範例會移除 Seattle Users 指派原則中的 MyVoicemail 管理角色，該角色可讓使用者管理其語音信箱選項。

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Users" -Role MyVoicemail | Remove-ManagementRoleAssignment

如需詳細的語法及參數資訊，請參閱 [Remove-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351205\(v=exchg.150\))。

