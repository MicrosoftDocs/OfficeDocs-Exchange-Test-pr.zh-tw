---
title: '檢視有效的權限: Exchange 2013 Help'
TOCTitle: 檢視有效的權限
ms:assetid: ae6cb7cf-f998-44a6-a69a-02ad736c8260
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638167(v=EXCHG.150)
ms:contentKeyID: 50473969
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視有效的權限

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-09_

在 Microsoft Exchange Server 2013會授與使用管理角色指派給管理角色群組、 管理角色指派原則、 通用安全性群組 (Usg)，或直接對使用者的權限。使用者都會授與的權限如果他們正在成員的角色群組或 Usg，或已指派的角色指派原則。

大部分的權限授與取決於角色群組成員資格或指派原則給使用者的工作分派。雖然使用角色群組和指派原則讓容易授與權限大量的使用者，您可能不知道誰是成員的角色群組，或被指派一個指派原則。這是其中**Get-ManagementRoleAssignment**指令程式上的*GetEffectiveUsers*參數是很有用。它會顯示您哪些使用者會授與指定的透過角色群組、 指派原則和指派給他們的 Usg 的管理角色的權限。

使用*Role*參數時*GetEffectiveUsers*參數可搭配**Get-ManagementRoleAssignment**指令程式。藉由指定此參數與特定角色， **Get-ManagementRoleAssignment**指令程式會檢查指定給的角色、 角色群組、 指派原則和 Usg，例如的所有角色 assignees，並列出每個成員。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>GetEffectiveUser</em>參數不會列出連結的外部索引角色群組之成員的使用者。而不是使用者的清單，如果找到連結的角色群組，就會顯示<strong>所有連結的群組成員</strong>。如需在多個樹系中的權限的詳細資訊，請參閱<a href="understanding-multiple-forest-permissions-exchange-2013-help.md">了解多重樹系權限</a>。</td>
</tr>
</tbody>
</table>


如需管理角色、 角色群組和指派原則的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。如需管理角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

要尋找與管理的權限相關的其他管理工作嗎？取出[權限](permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色群組」或「角色指派原則」項目。

  - 本主題中的程序只可以在命令介面中執行。您無法使用 Exchange 系統管理中心 (EAC) 來檢視有效的權限。

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


## 使用命令介面來列出所有有效的使用者

若要列出被授與管理角色所提供之權限的所有使用者，請使用下列語法。

    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers

此範例會列出被授與郵件收件者角色所提供之權限的所有使用者。

    Get-ManagementRoleAssignment -Role "Mail Recipients" -GetEffectiveUsers

如果您要變更清單中傳回的屬性，或是將清單匯出至逗號分隔值 (.csv) 檔案，請參閱本主題稍後的Use the Shell to customize output and display it。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 使用命令介面在某個角色上尋找特定使用者

若要尋找已授與權限的管理角色的特定使用者，必須使用**Get-ManagementRoleAssignment**指令程式來擷取所有的有效使用者的清單並接著將傳送到**Where**指令程式指令程式輸出。**Where**指令程式輸出會篩選並傳回您指定的使用者。使用下列語法。

    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

此範例會在日誌記錄角色上尋找使用者 David Strome。

    Get-ManagementRoleAssignment -Role Journaling -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" }

如果您要變更清單中傳回的內容，或是將清單匯出到 .csv 檔，請參閱本主題稍後的Use the Shell to customize output and display it。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 使用命令介面在所有角色上尋找特定使用者

了解每個使用者會收到將權限的角色，您必須使用**Get-ManagementRoleAssignment**指令程式來擷取所有的管理角色的所有有效使用者，然後將傳送到**Where**指令程式指令程式輸出。**Where**指令程式輸出會篩選並傳回僅授與使用者權限的角色指派。

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

此範例會尋找所有授與權限給使用者 Kim Akers 的角色指派。

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "Kim Akers" }

如果您要變更清單中傳回的內容，或是將清單匯出到 CSV 檔，請參閱本主題稍後的Use the Shell to customize output and display it。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 使用命令介面來自訂並顯示輸出

**Get-ManagementRoleAssignment**指令程式的預設輸出可能沒有您想要的資訊。Cmdlet 的輸出包含許多可存取的多個屬性。以下是一些屬性，可能會有幫助：

  - **EffectiveUserName**   使用者的名稱。

  - **角色**   授與權限的角色。

  - **RoleAssigneeName**   指派給角色的角色群組、指派原則或 USG，且包含 `EffectiveUserName` 屬性中的使用者。

  - **RoleAssigneeType**   表示角色是指派給角色群組、指派原則、USG 還是使用者。

  - **AssignmentMethod**   表示角色與角色受託人之間是直接還是間接指派關係。

  - **CustomRecipientWriteScope**  指出自訂收件者寫入範圍，如果有的話時建立套用至角色指派。此屬性中指定的範圍會覆寫`RecipientWriteScope`屬性中指定的隱含的收件者寫入範圍。

  - **CustomConfigWriteScope**  指出自訂組態寫入範圍，如果有的話時建立套用至角色指派。此屬性中指定的範圍會覆寫`ConfigWriteScope`屬性中指定隱含組態寫入範圍。

  - **RecipientReadScope**   表示套用至角色的隱含收件者讀取範圍。

  - **RecipientWriteScope**   表示套用至角色的隱含收件者寫入範圍。

  - **ConfigReadScope**   表示套用至角色的隱含組態讀取範圍。

  - **ConfigWriteScope**   表示套用至角色的隱含組態寫入範圍。

若要選取您想要顯示在清單中的屬性，您可以使用類似使用命令介面來列出所有有效使用者、使用命令介面來尋找上某個角色的特定使用者和使用命令介面來尋找上的所有角色的特定使用者的各節中所使用的命令。不同的是您將傳送至**Format-Table**或**Select-Object** cmdlet 這些命令的結果。**Format-Table** cmdlet 時十分有用輸出結果在畫面上的清單。**Select-Object** cmdlet 時十分有用輸出結果成.csv 檔案的清單。

這兩個指令程式可讓您指定您想要查看的屬性與您想要查看其順序。**Format-Table**指令程式可讓您更多選項時**Select-Object**不修改任何時將清單傳送至.csv 檔案是非常有用的方式中的輸出，列出在畫面上的結果。

如需 **Format-Table** 和 **Select-Object** 指令程式的相關資訊，請參閱 [使用命令輸出](working-with-command-output-exchange-2013-help.md)。

## 將自訂的清單輸出至畫面上

1.  選擇您要查看的資訊，並且從下列其中一個程序尋找相關聯的命令：
    
      - Use the Shell to list all effective users
    
      - Use the Shell to find a specific user a role
    
      - Use the Shell to find a specific user on all roles

2.  選擇要在清單中查看的內容。

3.  使用下列語法來檢視清單。
    
        <command to retrieve list > | Format-Table <property 1>, <property 2>, <property ...>

此範例會在所有角色中尋找使用者 David Strome，並且顯示 `EffectiveUserName`、`Role`、`CustomRecipientWriteScope` 和 `CustomConfigWriteScope` 內容。

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Format-Table EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 將自訂的清單輸出至 .csv 檔案

若要將清單匯出成.csv 檔案，您需要將傳送到**Select-Object**指令程式先前所列的適當程序從**Get-ManagementRoleAssignment**命令的結果。**Select-Object**指令程式的輸出接著會傳送到**Export-CSV**指令程式，這會.csv 輸出儲存到您指定的檔案名稱。

1.  選擇您要查看的資訊，並且從下列其中一個程序尋找相關聯的命令：
    
      - Use the Shell to list all effective users
    
      - Use the Shell to find a specific user a role
    
      - Use the Shell to find a specific user on all roles

2.  選擇要在清單中查看的內容。

3.  使用下列語法將清單匯出至 .csv 檔案。
    
        <command to retrieve list > | Select-Object <property 1>, <property 2>, <property ...> | Export-CSV <filename>

此範例會在所有角色中尋找使用者 David Strome，並且顯示 `EffectiveUserName`、`Role`、`CustomRecipientWriteScope` 和 `CustomConfigWriteScope` 內容。

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Select-Object EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope | Export-CSV c:\output.csv

您現在可以在自己選擇的檢視器中檢視 .csv 檔案。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

