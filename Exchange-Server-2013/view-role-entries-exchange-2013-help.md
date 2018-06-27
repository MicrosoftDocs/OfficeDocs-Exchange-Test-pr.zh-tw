---
title: '檢視角色項目: Exchange 2013 Help'
TOCTitle: 檢視角色項目
ms:assetid: d9bb0d14-db59-456c-8f50-a8d7f7323df9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351179(v=EXCHG.150)
ms:contentKeyID: 50474371
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視角色項目

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

每個管理角色項目代表單一 cmdlet 或指令碼。角色項目中包含的參數會決定使用者可以存取哪些參數 cmdlet 或指令碼上。

角色項目的身分識別是由關聯的角色項目、 管理角色名稱的指令程式或指令碼角色項目參照所組成。如需 Microsoft Exchange Server 2013中的角色項目的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

要尋找與角色項目相關的其他管理工作嗎？取出[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理角色」項目。

  - 您必須使用命令介面來執行這些程序。

  - 本主題會使用管線、 **Format-List**指令程式、 物件和屬性。如需這些概念的詳細資訊，請參閱下列主題：
    
      - [管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))
    
      - [使用命令輸出](working-with-command-output-exchange-2013-help.md)
    
      - [結構化的資料](https://technet.microsoft.com/zh-tw/library/aa996386\(v=exchg.150\))

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

## 檢視角色項目的清單

您可以使用**Get-ManagementRoleEntry**指令程式來擷取的角色項目清單。當您使用**Get-ManagementRoleEntry**指令程式時，您必須指定包含兩個角色名稱包含您想要清單中的角色項目以及您想要列出角色項目的指令程式名稱的值。您可以藉由結合的角色名稱和指令程式名稱和萬用字元 （\*），傳回特定或廣泛的角色項目清單。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd335210\(v=exchg.150\))。

## 檢視角色上所有角色項目的清單

若要檢視特定角色上角色項目的清單，請使用下列語法。

    Get-ManagementRoleEntry <role name>\*

此範例會擷取 `Recipient Administrators` 角色上的所有角色項目。

    Get-ManagementRole "Recipient Administrators\*"

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd335210\(v=exchg.150\))。

## 檢視包含特定角色項目之角色的清單

若要檢視所有包含特定角色項目之角色的清單，請使用下列語法。

    Get-ManagementRoleEntry *\<cmdlet name>

此範例會擷取所有包含 **Set-Mailbox** 角色項目的角色。

    Get-ManagementRoleEntry *\Set-Mailbox

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd335210\(v=exchg.150\))。

## 檢視包含類似角色項目之目標角色的清單

若要檢視包含具有類似名稱的指令程式之目標角色的清單，請使用下列語法。

    Get-ManagementRoleEntry *<partial role name>*\*<partial cmdlet name>*

此範例會針對名稱包含字串 `Tier 1` 的角色，傳回這些角色上包含字串 `Mailbox` 之角色項目的清單。

    Get-ManagementRoleEntry "*Tier 1*\*Mailbox*"

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd335210\(v=exchg.150\))。

## 檢視單一角色項目

若要檢視單一角色項目的詳細資料，請使用下列語法。

    Get-ManagementRoleEntry <role name>\<cmdlet name> | Format-List

此範例會擷取 `Recipient Administrators` 角色上 **Set-Mailbox** 角色項目的詳細資料。

    Get-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" | Format-List

如果您使用 **Format-List** 指令程式時，檢視的角色項目有太多參數要列出，請參閱本主題稍後的＜檢視單一角色項目上的參數＞。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd335210\(v=exchg.150\))。

## 檢視單一角色項目上的參數

某些角色項目有多個參數比可以檢視透過管線傳送 format-list **Get-ManagementRoleEntry**指令程式在**Format-List** cmdlet 的結果。如果您要檢視的角色項目上的所有參數，您需要直接存取角色項目物件的**Parameters**屬性。

若要檢視角色項目物件的 **Parameters** 內容上儲存的參數，請使用下列語法。

    (Get-ManagementRoleEntry <role name>\<cmdlet name>).Parameters

此範例會擷取「郵件收件者」角色上 **Set-Mailbox** 角色項目的參數。

    (Get-ManagementRoleEntry "Mail Recipients\Set-Mailbox").Parameters

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-tw/library/dd335210\(v=exchg.150\))。

