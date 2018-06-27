---
title: '管理角色群組: Exchange 2013 Help'
TOCTitle: 管理角色群組
ms:assetid: ab9b7a3b-bf67-4ba1-bde5-8e6ac174b82c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657480(v=EXCHG.150)
ms:contentKeyID: 50473962
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理角色群組

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-08_

本主題顯示如何新增、 移除、 複製及檢視 Microsoft Exchange Server 2013中的管理角色群組。它也會顯示如何新增、 移除及列出在角色群組的管理角色以及如何變更管理範圍和角色群組的代理人。如需Exchange 2013中的角色群組的詳細資訊，請參閱[了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)。

若欲瞭解更多與角色群組相關的管理工作，請參閱 [權限](permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成每項程序預估時間： 5 到 10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色群組」項目。

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

## 建立角色群組

如果您想自訂可以指派給使用者群組的權限，請建立新的自訂管理角色群組。

## 使用 EAC 建立角色群組

1.  在 Exchange 系統管理中心 (EAC) 中，導覽至 \[權限\] \> \[管理員角色\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[新角色群組\] 視窗中，為新角色群組提供名稱。

3.  您可以選取要指派給角色群組的角色，以及現在要新增至角色群組的成員，或是之後再這樣做。

4.  選取要套用到新角色群組的寫入範圍。

5.  按一下 \[儲存\] 以建立角色群組。

## 使用命令介面建立角色群組

若要建立角色群組，請參閱 [New-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638181\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-tw/dd638181\(exchg.150\)#examples)區段。

## 如何才能了解這是否正常運作？

若要確認是否已成功建立角色群組，請執行下列操作：

1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  確認新的角色群組出現在角色群組清單中，然後選取該群組。

3.  確認您在新角色群組上指定的成員、指派角色和範圍都列在角色群組詳細資料窗格中。

## 複製角色群組

## 使用 EAC 複製角色群組

如果您擁有的角色群組包含要授予使用者的權限，但是您希望套用其他管理範圍，或者希望移除或新增一個或兩個管理角色，而不必手動新增所有其他角色，則可以複製現有角色群組。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 將複製的角色群組若您使用Exchange管理命令介面來設定多個管理角色範圍或獨佔範圍的角色群組上。如果您已設定多個範圍或獨佔範圍的角色群組上，您必須使用本主題稍後的命令介面程序將複製的角色群組。如需管理角色範圍的詳細資訊，請參閱<a href="understanding-management-role-scopes-exchange-2013-help.md">了解管理角色範圍</a>。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取您要複製的角色群組，然後按一下 \[複製\]![複製圖示](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "複製圖示")。

3.  在 \[新角色群組\] 視窗中，為新角色群組提供名稱。

4.  檢閱已複製到新的角色群組的角色。新增或移除做為必要的角色。

5.  檢閱寫入範圍，並視需要進行變更。

6.  檢閱已複製到新的角色群組的成員。新增或移除做為所需的成員。

7.  按一下 \[儲存\] 以建立角色群組。

## 使用命令介面複製沒有範圍的角色群組

1.  使用下列語法將您要複製的角色群組儲存到變數中。
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  使用以下語法建立新角色群組，新增成員至該角色群組，並指定誰可以將新角色群組委派給其他使用者。
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -Members <member1, member2, member3...> -ManagedBy <user1, user2, user3...>

例如，下列命令複製組織管理角色群組，並命名為新的角色群組的 「 有限的組織管理 」。它會新增成員 Isabelle、 Carter、 及 Lukas 並可由黎和產業 katie 了委派。

    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Limited Organization Management" -Roles $RoleGroup.Roles -Members Isabelle, Carter, Lukas -ManagedBy Jenny, Katie

建立新角色群組之後，您可以新增或移除角色、變更角色上角色指派的範圍以及進行其他作業。

如需詳細的語法及參數資訊，請參閱 [Get-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638115\(v=exchg.150\)) 與 [New-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638181\(v=exchg.150\))。

## 使用命令介面複製具有自訂範圍的角色群組

1.  使用下列語法將您要複製的角色群組儲存到變數中。
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  使用下列語法建立具有自訂範圍的新角色群組。
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuraiton scope name>

例如，以下命令將複製 Organization Management 角色群組，並建立名為 Vancouver Organization Management 的新角色群組，新群組的收件者範圍是 Vancouver Users，組態範圍是 Vancouver Servers。

    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Vancouver Organization Management" -Roles $RoleGroup.Roles -CustomRecipientWriteScope "Vancouver Users" -CustomConfigWriteScope "Vancouver Servers"

您也可以新增成員至角色群組時使用*Members*參數所示使用命令介面來複製角色群組範圍無法使用本主題前述所建立。如需管理範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

建立新角色群組之後，您可以新增或移除角色、變更角色上角色指派的範圍以及執行其他工作。

如需詳細的語法及參數資訊，請參閱 [Get-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638115\(v=exchg.150\)) 與 [New-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638181\(v=exchg.150\))。

## 使用命令介面複製具有 OU 範圍的角色群組

1.  使用下列語法將您要複製的角色群組儲存到變數中。
    
        $RoleGroup = Get-RoleGroup <name of role group to copy>

2.  使用下列語法建立具有自訂範圍的新角色群組。
    
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope <OU name>

例如，以下命令將複製 Recipient Management 角色群組，並建立名為 Toronto Recipient Management 的新角色群組，新群組僅允許對 Toronto Users OU 中的使用者進行管理。

    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Toronto Recipient Management" -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope "contoso.com/Toronto Users"

您也可以新增成員至角色群組時使用*Members*參數所示使用命令介面來複製角色群組範圍無法使用本主題前述所建立。如需管理範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

建立新角色群組之後，您可以新增或移除角色、變更角色上角色指派的範圍以及進行其他作業。

如需詳細的語法及參數資訊，請參閱 [Get-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638115\(v=exchg.150\)) 與 [New-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638181\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功複製角色群組，請執行下列操作：

1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  確認複製的角色群組出現在角色群組清單中，然後選取該群組。

3.  確認您在複製的角色群組上指定的成員、指派角色和範圍都列在角色群組詳細資料窗格中。

## 移除角色群組

如果您不再需要您建立的角色群組，您可以將它移除。當您移除的角色群組時，會刪除角色群組和管理角色之間的管理角色指派。管理角色不刪除。如果使用者相依於角色群組的存取功能，使用者將不再有該功能的存取。您無法移除內建角色群組。

## 使用 EAC 移除角色群組

1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取您要移除的角色群組，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

3.  確認您要移除選取的角色群組，如果確定，則對警告回應 \[是\]。

## 使用命令介面移除角色群組

若要移除角色群組，請參閱 [Remove-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638141\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-tw/dd638141\(exchg.150\)#examples)區段。

## 檢視角色群組

您可以檢視組織中的角色群組清單或特定角色群組的詳細資訊。

## 使用 EAC 檢視角色群組清單和角色群組詳細資料

1.  在 EAC 中，瀏覽至 \[**權限**\>**系統管理員角色**。以下會列出所有在組織中的角色群組。

2.  選取一個角色群組，以檢視針對該角色群組設定的成員、指派角色和範圍。

## 使用命令介面檢視角色群組清單和角色群組詳細資料

若要檢視角色群組清單，請參閱 [Get-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638115\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-tw/dd638115\(exchg.150\)#examples)區段。

## 將角色新增至角色群組

將管理角色新增至角色群組是系統管理員或專家使用者的群組權限授與最佳且最簡單的方式。如果您想要授與成員角色群組讓您管理功能的使用者，您會新增管理角色群組的功能的管理角色。新增角色之後，角色群組的成員會授與角色所提供的權限。

## 使用 EAC 將管理角色新增至角色群組

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 將角色新增至角色群組若您使用命令介面來設定多個管理角色範圍或獨佔範圍的角色群組上。如果您已設定多個範圍或獨佔範圍的角色群組上，您必須使用本主題稍後的命令介面程序將角色新增至角色群組。如需管理角色範圍的詳細資訊，請參閱<a href="understanding-management-role-scopes-exchange-2013-help.md">了解管理角色範圍</a>。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取要在其中新增角色的角色群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[角色\] 區段中，選取要新增至角色群組的角色。

4.  將角色新增至角色群組完成之後，按一下 \[儲存\]。

## 使用命令介面來建立不具有範圍的角色指派

您可以建立角色指派角色和角色群組之間的任何範圍。當您這樣做時，不明確的讀取和隱含寫入範圍的角色套用。

使用下列語法來將沒有任何範圍的角色指派給角色群組。如果您沒有指定一個，會自動建立角色指派名稱。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name>

本範例將「傳輸規則」管理角色指派給「西雅圖規範」角色群組。

    New-ManagementRoleAssignment -SecurityGroup "Seattle Compliance" -Role "Transport Rules"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 使用命令介面來建立具有預先定義之範圍的角色指派

如果預先定義的範圍符合您的業務需求，您可以將該範圍套用至角色指派，而不是建立一個新。如需預先定義的範圍和及其描述的清單，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

如需角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

使用下列語法來將角色指派給角色群組與預先定義的範圍。如果您沒有指定一個，會自動建立角色指派名稱。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientRelativeWriteScope < MyGAL | MyDistributionGroups | Organization | Self >

本範例將「郵件追蹤」角色指派給「企業支援」角色群組，並套用「組織」預先定義的範圍。

    New-ManagementRoleAssignment -SecurityGroup "Enterprise Support" -Role "Message Tracking" -RecipientRelativeWriteScope Organization

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 使用命令介面來建立具有以收件者篩選器為基礎之範圍的角色指派

如果您建立以收件者篩選器為基礎的範圍，則在用來指派角色給角色群組的命令中，您必須使用 *CustomRecipientWriteScope* 參數來包含該範圍。

當您建立具有收件者寫入範圍的角色指派時，您也可以包含組態寫入範圍。

如需角色指派和範圍的詳細資訊，請參閱下列主題：

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

使用下列語法來指派角色給收件者篩選器型範圍的角色群組。如果您沒有指定一個，會自動建立角色指派名稱。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomRecipientWriteScope <role scope name>

本範例將「郵件追蹤」角色指派給「西雅圖收件者管理員」角色群組，並套用「西雅圖收件者」範圍。

    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Message Tracking" -CustomRecipientWriteScope "Seattle Recipients"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 使用命令介面建立具有組態範圍的角色指派

如果您建立了伺服器或資料庫組態篩選器或清單型範圍，必須使用 *CustomConfigWriteScope* 參數，在用來指派角色至角色群組的命令中包含範圍。

當您建立具有組態寫入範圍的角色指派時，您也可以包含收件者寫入範圍。

如需角色指派和管理範圍的詳細資訊，請參閱下列主題：

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

使用下列語法來指派角色給組態範圍的角色群組。如果您沒有指定一個，會自動建立角色指派名稱。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <role scope name>

本範例將「資料庫」角色指派給「西雅圖伺服器管理員」角色群組，並套用「西雅圖伺服器」範圍。

    New-ManagementRoleAssignment -SecurityGroup "Seattle Server Admins" -Role "Databases" -CustomConfigWriteScope "Seattle Servers"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 使用命令介面來建立具有 OU 範圍的角色指派

如果您要將角色的寫入範圍設為某個 OU，您可以直接在 *RecipientOrganizationalUnitScope* 參數中指定該 OU。

如需角色指派和管理範圍的詳細資訊，請參閱下列主題：

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

使用下列命令，將角色指派給角色群組和角色寫入範圍限制在特定 OU。如果您沒有指定一個，會自動建立角色指派名稱。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientOrganizationalUnitScope <OU>

本範例將「郵件收件者」角色指派給「西雅圖收件者管理員」角色群組，並將指派的範圍設定為 Contoso.com 網域中的銷售\\使用者 OU。

    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功將角色新增至角色群組，請執行下列操作：

1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取 \[新增角色的角色群組。在角色群組詳細資料窗格中，確認您已新增的角色列出。

## 移除角色群組中的角色

移除管理角色群組的角色是最佳最簡單方式撤銷權限授與給系統管理員或專家使用者的群組。如果您不想系統管理員或專家使用者有權限管理功能，您移除管理角色管理的權限的管理角色群組。移除角色之後，角色群組的成員將不再有管理該功能的權限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>部分的角色群組，例如組織管理角色群組中，限制哪些角色可以從角色群組中移除。如需詳細資訊，請參閱<a href="understanding-management-role-groups-exchange-2013-help.md">了解管理角色群組</a>。<br />
如果系統管理員是另一個角色群組的成員，此群組包含授與權限來管理此功能的管理角色，則您需要從其他角色群組中移除系統管理員，或從其他角色群組中移除負責授與權限來管理此功能的角色。</td>
</tr>
</tbody>
</table>


## 使用 EAC 從角色群組中移除管理角色

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 如果您使用命令介面來設定多個範圍或獨佔範圍上的角色群組角色移除角色群組。如果您已設定多個範圍或獨佔範圍的角色群組上，您必須使用本主題稍後的命令介面程序來移除角色群組中的角色。如需管理角色範圍的詳細資訊，請參閱<a href="understanding-management-role-scopes-exchange-2013-help.md">了解管理角色範圍</a>。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取要移除其中所含角色的角色群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[角色\] 區段中，選取要從角色群組中移除的角色。

4.  從角色群組中移除角色完成之後，按一下 \[儲存\]。

## 使用命令介面從角色群組中移除角色

您可以移除角色群組角色擷取使用**Get-ManagementRoleAssignment**指令程式和角色指派給**Remove-ManagementRoleAssignment**指令程式傳回然後 piping 相關的管理角色指派。除非您想要同時移除委派和一般角色指派，指定*Delegating*參數指定是否要移除規則或委派角色指派。

如需一般和委派角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

此程序會使用管線。如需以管線傳送的詳細資訊，請參閱[管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))。

若要從角色群組中移除角色，請使用下列語法。

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment

本範例會移除通訊群組的角色，讓管理員能夠管理通訊群組、 西雅圖 Recipient Administrators 角色群組。因為我們想要移除提供管理通訊群組的權限的角色指派， *Delegating*參數會設為`$False`，這只會傳回一般角色指派。

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Recipient Administrators" -Role "Distribution Groups" -Delegating $false | Remove-ManagementRoleAssignment

如需詳細的語法及參數資訊，請參閱 [Remove-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351205\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功從角色群組中移除角色，請執行下列操作：

1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取移除從角色的角色群組。在角色群組的 \[詳細資料\] 窗格中，確認已不再列出您移除的角色。

## 變更角色群組的範圍

角色群組和角色之間的管理角色指派包含管理範圍，決定何種物件給該角色群組的成員可提供使用。透過變更寫入範圍的角色群組，您可以變更哪些物件會對可用來建立、 變更或移除的角色群組成員。您無法變更角色群組上的讀取的範圍。

Exchange 2013包含範圍會套用預設角色指派時所不建立的任何自訂的範圍。如果您想要使用自訂的範圍與角色指派的角色群組，您必須建立一個第一個。如需詳細資訊建立自訂範圍進階工作，請參閱[建立規則或獨佔範圍](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

如需 Exchange 2013 中的管理角色範圍和指派的詳細資訊，請參閱下列主題：

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

## 使用 EAC 變更角色群組的範圍

當您使用 EAC 來變更範圍的角色群組時、 您要實際變更角色群組和每個管理角色指派給角色群組之間的所有角色指派的範圍。如果您想要變更特定角色指派的範圍，您必須使用命令介面程序本主題稍後的。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 中，如果您已使用命令介面在這些角色指派上設定多個範圍或獨佔範圍管理角色和角色群組之間的角色指派範圍。如果您已在這些角色指派上設定多個範圍或獨佔範圍，您必須使用本主題稍後的命令介面程序來管理範圍。如需管理角色範圍的詳細資訊，請參閱<a href="understanding-management-role-scopes-exchange-2013-help.md">了解管理角色範圍</a>。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取您要變更其範圍的角色群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在以下兩個 **\[寫入範圍\]** 選項中，選取其中之一：
    
      - 下拉式方塊中的寫入範圍，您可以在其中選取預設寫入範圍或自訂寫入範圍。
    
      - **組織單位** 如果您要將此角色群組的範圍設為組織單位 (OU)，請選取此選項並提供組織單位。

4.  按一下 \[儲存\]，將變更儲存到角色群組。

## 使用命令介面同時在角色群組上變更所有角色指派的範圍

角色指派的角色群組和指派給該角色之間可以使用其本身、 相同的自訂範圍或不同的自訂範圍取自角色隱含範圍。如需角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

使用**Set-ManagementRoleAssignment**指令程式來管理角色指派的範圍。您不能管理使用**Set-RoleGroup**指令程式的範圍。

若要在同一時間變更角色群組和管理角色的一組之間的所有角色指派的範圍，您必須先擷取在角色群組、 角色指派然後在每個工作分派設定新的範圍。您可以使用**Get-ManagementRoleAssignment**指令程式來擷取的角色指派，這樣並再將它們傳送到**Set-ManagementRoleAssignment**指令程式。

此程序會使用管線的概念和*WhatIf*參數。如需詳細資訊，請參閱下列主題：

  - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))

  - [WhatIf、Confirm 及 ValidateOnly 參數](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

若要同時在角色群組上的所有角色指派上設定範圍，請使用以下語法。

    Get-ManagementRoleAssignment -RoleAssignee <name of role group> | Set-ManagementRoleAssignment -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>

您使用僅參數則需要設定想要使用的範圍。例如，如果您想要變更 「 銷售收件者管理 」 角色群組上的所有角色指派的收件者範圍為直接銷售員工，使用下列命令。

    Get-ManagementRoleAssignment -RoleAssignee "Sales Recipient Management" | Set-ManagementRoleAssignment -CustomRecipientWriteScope "Direct Sales Employees"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用<em>WhatIf</em>參數來確認已變更只想要變更的角色指派。執行上述命令與<em>WhatIf</em>參數以確認結果，並移除<em>WhatIf</em>交換器以套用變更。</td>
</tr>
</tbody>
</table>


如需變更管理角色指派的詳細資訊，請參閱[變更角色指派](change-a-role-assignment-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 使用命令介面在角色群組上變更個別角色指派的範圍

角色指派的角色群組和指派給該角色之間可以使用其本身、 相同的自訂範圍或不同的自訂範圍取自角色隱含範圍。如需角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

使用**Set-ManagementRoleAssignment**指令程式來管理角色指派的範圍。您不能管理使用**Set-RoleGroup**指令程式的範圍。

管線的概念和**Format-List**指令程式會使用此程序。如需詳細資訊，請參閱下列主題：

  - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))

  - [使用命令輸出](working-with-command-output-exchange-2013-help.md)

若要在角色群組和管理角色之間的角色指派上變更範圍，您必須先找到角色指派的名稱，然後在角色指派上設定範圍。

1.  若要尋找名稱的所有角色指派的角色群組，請使用下列命令。透過管線傳送 format-list 管理角色指派給**Format-List**指令程式，您可以檢視工作分派的完整名稱。
    
        Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-List Name

2.  尋找您想要變更角色指派的名稱。下一個步驟中使用的角色指派的名稱。

3.  若要在個別指派上設定範圍，請使用下列語法。
    
        Set-ManagementRoleAssignment <role assignment name> -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>

您使用僅參數則需要設定想要使用的範圍。例如，如果您想要變更收件者範圍的郵件 Recipients\_Sales 收件者管理角色指派給所有銷售員工，使用下列命令。

    Set-ManagementRoleAssignment "Mail Recipients_Sales Recipient Management" -CustomRecipientWriteScope "All Sales Employees"

如需變更管理角色指派的詳細資訊，請參閱[變更角色指派](change-a-role-assignment-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱 [Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認已成功變更角色群組中角色指派的範圍，請執行下列操作：

  - 如果您使用 EAC 設定角色群組的範圍，請執行下列操作：
    
    1.  在 EAC 中，瀏覽至 \[**權限**\>**系統管理員角色**。以下列出您組織中的所有角色群組。
    
    2.  選取角色群組，以檢視對角色群組設定的範圍。

  - 如果您使用命令介面設定角色群組的範圍，請執行下列操作：
    
    1.  在命令介面中執行下列命令。
        
            Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-Table *WriteScope
    
    2.  確認角色指派的寫入範圍已變更為您指定的範圍。

## 新增或移除角色群組委派

角色群組代理人的使用者或萬用安全性群組 (Usg)，可以新增或移除角色群組的成員或變更角色群組的屬性。新增或移除角色群組代理人，您可以控制人來管理角色群組。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您新增代理人到角色群組之後，僅能由角色群組上的代理人或指派的使用者直接或間接、以角色對角色來管理角色群組。<br />
如果已直接或間接指派使用者，即不會新增「角色管理」角色做為角色群組的代理人，使用者必須使用 <strong>Add-RoleGroupMember</strong>、<strong>Remove-RoleGroupMember</strong>、<strong>Update-RoleGroupMember</strong> 及 <strong>Set-RoleGroup</strong> Cmdlet 上的 <em>BypassSecurityGroupManagerCheck</em> 參數來管理角色群組。</td>
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
<td>您無法使用 EAM 將委派新增至角色群組。</td>
</tr>
</tbody>
</table>


## 使用命令介面新增代理人到角色群組

若要變更代理人的角色群組的清單，您可以使用*ManagedBy*參數**Set-RoleGroup**指令程式上。*ManagedBy*參數會覆寫在角色群組的整個委派清單。如果您想要新增的角色的代理人群組而不取代整個代理人清單，請使用下列步驟：

1.  使用下列命令，透過變數儲存角色群組。
    
        $RoleGroup = Get-RoleGroup <role group name>

2.  使用以下命令新增代理人到儲存於變數中的角色群組。
    
        $RoleGroup.ManagedBy += (Get-User <user to add>).Identity
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您想新增 USG，請使用 <strong>Get-Group</strong> Cmdlet。</td>
    </tr>
    </tbody>
    </table>


3.  重複步驟 2 來新增其他代理人。

4.  使用下列命令，將新的委派清單套用至實際的角色群組。
    
        Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy

此範例會在 組織管理 角色群組上新增使用者 David Strome 以做為代理人。

    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy += (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy

如需詳細的語法及參數資訊，請參閱 [Set-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638182\(v=exchg.150\))。

## 使用命令介面來移除角色群組中的代理人

若要變更代理人的角色群組的清單，您可以使用*ManagedBy*參數**Set-RoleGroup**指令程式上。*ManagedBy*參數會覆寫在角色群組的整個委派清單。若要從角色群組中移除代理人而不是取代整個代理人清單，請使用下列步驟：

1.  使用下列命令，透過變數儲存角色群組。
    
        $RoleGroup = Get-RoleGroup <role group name>

2.  使用以下命令移除儲存於變數中之角色群組的代理人。
    
        $RoleGroup.ManagedBy -= (Get-User <user to remove>).Identity
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您想移除 USG，請使用 <strong>Get-Group</strong> Cmdlet。</td>
    </tr>
    </tbody>
    </table>


3.  重複步驟 2 來移除其他代理人。

4.  使用下列命令，將新的委派清單套用至實際的角色群組。
    
        Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy

此範例會移除在 組織管理 角色群組做為代理人的使用者 David Strome。

    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy -= (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy

如需詳細的語法及參數資訊，請參閱 [Set-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638182\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功變更角色群組上的委派清單，請執行下列操作：

1.  在命令介面中，執行下列命令。
    
        Get-RoleGroup <role group name> | Format-List ManagedBy

2.  確認 *ManagedBy* 內容上列出的委派僅包含能夠管理角色群組的委派。

