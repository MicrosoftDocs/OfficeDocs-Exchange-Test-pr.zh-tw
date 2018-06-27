---
title: '檢視角色指派: Exchange 2013 Help'
TOCTitle: 檢視角色指派
ms:assetid: 0be4def9-af6d-476a-9c97-7155ae11b587
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335086(v=EXCHG.150)
ms:contentKeyID: 50472537
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視角色指派

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

管理角色指派給角色受託人指派管理角色。如需 Microsoft Exchange Server 2013中的管理角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色指派」項目。

  - 您必須使用命令介面來執行這些程序。

  - 本主題會使用管線及**Format-List**指令程式。如需這些概念的詳細資訊，請參閱下列主題：
    
      - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))
    
      - [使用命令輸出](working-with-command-output-exchange-2013-help.md)

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

## 檢視所有角色指派的清單

您可以檢視執行**Get-ManagementRoleAssignment**指令程式來設定在組織中的所有角色指派的清單。如果您想要擷取的角色指派符合您指定的部分字串清單，使用萬用字元 （\*）。此範例會擷取開頭字串"層 1"的所有角色指派的清單。

    Get-ManagementRoleAssignment "Tier 1*"

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視特定角色指派的詳細資料

您可以透過管線傳送 format-list **Get-ManagementRoleAssignment**指令程式在**Format-List** cmdlet 的結果檢視角色指派的詳細資料。使用下列語法。

    Get-ManagementRoleAssignment <assignment name> | Format-List

此範例會擷取「服務台指派」角色指派的詳細資料。

    Get-ManagementRoleAssignment "Help Desk Assignment" | Format-List

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視指派給特定角色受託人之角色指派的清單

若要檢視與管理角色群組、角色或角色指派原則關聯之角色指派的清單，或與使用者或萬用安全性群組 (USG) 關聯之角色指派的清單，請使用下列語法。

    Get-ManagementRoleAssignment -RoleAssignee <role assignee name>

此範例會擷取與「伺服器管理」角色群組關聯的所有角色指派。

    Get-ManagementRoleAssignment -RoleAssignee "Server Management"

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視與特定角色相關聯的角色指派

每個角色可以有多個角色指派。您可以使用**Get-ManagementRoleAssigment**指令程式來檢視與指定的角色相關聯的角色指派的清單。

若要檢視與指定角色相關聯之角色指派的清單，請使用下列語法。

    Get-ManagementRoleAssignment -Role <role name>

此範例會擷取與「郵件收件者」角色關聯的所有角色指派。

    Get-ManagementRoleAssignment -Role "Mail Recipients"

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視使用特定預先定義範圍之角色指派的清單

若要檢視使用特定預先定義範圍之角色指派的清單，請使用下列語法。

    Get-ManagementRoleAssignment -RecipientWriteScope < MyGAL | MyDistributionGroups | Organization | Self | CustomRecipientScope | ExecutiveRecipientScope >

此範例會擷取使用「組織」預先定義範圍的所有角色指派。

    Get-ManagementRoleAssignment -RecipientWriteScope Organization

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視範圍已被限定為特定 OU 之角色指派的清單

若要檢視範圍已被限定為特定組織單位 (OU) 之角色指派的清單，請使用下列語法。

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope <OU>

此範例會擷取在 contoso.com 網域中範圍已被限定為 North America\\Engineering\\Users OU 的所有角色指派。

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope "contoso.com/North America/Engineering/Users"

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視使用特定自訂範圍之指派的清單

若要檢視的使用特定的自訂範圍的角色指派清單，您必須先判斷範圍是否收件者範圍、 設定範圍、 獨佔的收件者範圍或獨佔組態範圍。每種類型的範圍會**Get-ManagementRoleAssignment**指令程式上使用不同的參數。以下列出每個範圍和其相關聯的參數：

  - **收件者範圍**   *CustomRecipientWriteScope*

  - **組態範圍**   *CustomConfigWriteScope*

  - **獨佔收件者範圍**   *ExclusiveRecipientWriteScope*

  - **獨佔組態範圍**   *ExclusiveConfigWriteScope*

每個參數的語法為相同。使用比對的範圍是類型參數指定範圍的名稱。

此範例會擷取使用「溫哥華收件者」收件者範圍的所有角色指派。

    Get-ManagementRoleAssignment -CustomRecipientWriteScope "Vancouver Recipients"

此範例會擷取使用「西雅圖 AD 站台」獨佔組態範圍的所有角色指派。

    Get-ManagementRoleAssignment -ExclusiveConfigWriteScope "Seattle AD Site"

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視獨佔或一般範圍的清單

若要檢視獨佔或一般角色指派的清單，請使用下列語法。

    Get-ManagementRoleAssignment -Exclusive < $True | $False >

例如，若要檢視獨佔範圍的清單，請執行下列命令：

    Get-ManagementRoleAssignment -Exclusive $True

此範例會擷取一般範圍的清單，而不含任何獨佔範圍。

    Get-ManagementRoleAssignment -Exclusive $False

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視特定收件者或伺服器的修改者

若要檢視特定收件者或伺服器可以修改角色指派清單，請使用*WritableRecipient*和*WritableServer*參數。指定收件者的名稱與*WritableRecipient*參數和*WritableServer*參數與伺服器的名稱。

此範例會擷取可以修改收件者 Brian 之角色指派的清單。

    Get-ManagementRoleAssignment -WritableRecipient "Brian"

您可以合併*WritableRecipient*和*WritableServer*參數的其他參數，例如*RoleAssignee*參數和*GetEffectiveUsers*切換精簡查詢並依序展開 \[任何角色群組或 Usg。本範例會擷取所有使用者誰可以修改 server EX02 與人員指派給伺服器管理角色群組。

    Get-ManagementRoleAssignment -WritableServer EX02 -RoleAssignee "Server Management" -GetEffectiveUsers

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視透過角色群組或 USG 從指派接收權限的使用者

若要檢視從角色指派接收權限之使用者的清單，請使用下列語法。

    Get-ManagementRoleAssignment <assignment name> -GetEffectiveUsers

此範例會擷取「服務台指派」角色指派中使用者的清單。

    Get-ManagementRoleAssignment "Help Desk Assignment" -GetEffectiveUsers

您也可以結合*GetEffectiveUsers*交換器與**Get-ManagementRoleAssignment**指令程式來展開角色群組和 Usg 已指派的角色指派上的數個其他參數。*GetEffectiveUsers*交換器與其他參數的使用方式的範例，請參閱本主題中前面的 「 可以修改特定收件者或伺服器檢視"。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

## 檢視已啟用或已停用之角色指派的清單

若要檢視已啟用或已停用之角色指派的清單，請使用下列語法。

    Get-ManagementRoleAssignment -Enabled < $True | $False >

此範例會擷取已停用之角色指派的清單。

    Get-ManagementRoleAssignment -Enabled $False

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

