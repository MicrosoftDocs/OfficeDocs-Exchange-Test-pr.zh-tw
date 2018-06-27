---
title: '檢視角色: Exchange 2013 Help'
TOCTitle: 檢視角色
ms:assetid: 1875b15f-22db-4ede-b310-ea894d6211c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335117(v=EXCHG.150)
ms:contentKeyID: 50472639
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視角色

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

管理角色可以各種方式，根據您想要的資訊列。例如，您可以選擇傳回特定角色類型、 只包含特定的 cmdlet 與參數的角色的角色或檢視特定的管理角色的詳細資料。如需 Microsoft Exchange Server 2013中的管理角色的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

如果您要檢視角色的所有管理角色項目清單，請參閱[檢視角色項目](view-role-entries-exchange-2013-help.md)。

要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理角色」項目。

  - 您必須使用命令介面來執行這些程序。

  - 本主題會使用管線和**Format-List**和**Format-Table**指令程式。如需這些概念的詳細資訊，請參閱下列主題：
    
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

## 檢視特定的管理角色

您也可以使用 **Get-ManagementRole** Cmdlet 並將輸出以管線傳送至 **Format-List** Cmdlet 來擷取特定角色，以檢視特定角色的詳細資料。

若要檢視特定角色的詳細資料，請使用下列語法。

    Get-ManagementRole <role name> | Format-List

此範例會擷取 Mail Recipients 管理角色的詳細資料。

    Get-ManagementRole "Mail Recipients" | Format-List

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351125\(v=exchg.150\))。

## 列出所有管理角色

您可以藉由執行**Get-ManagementRole**指令程式時未指定任何角色來檢視您組織中的所有管理角色的清單。根據預設，每個角色的角色類型與角色名稱會包含在結果中。

此範例會傳回您組織中所有角色的清單。

    Get-ManagementRole

若要傳回組織中的特定內容的所有角色清單，您可以將傳送**Format-Table** cmdlet 的結果，並指定您想要的屬性清單中的結果。使用下列語法。

    Get-ManagementRole | Format-Table <property 1>, <property 2...>

此範例會傳回您組織中所有角色的清單，並包含 **Name** 內容及內容名稱開頭具有 **Implicit** 字眼的任何內容。

    Get-ManagementRole | Format-Table Name, Implicit*

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351125\(v=exchg.150\))。

## 列出包含特定 Cmdlet 的管理角色

您可以透過在 **Get-ManagementRole** Cmdlet 上使用 *Cmdlet* 參數來傳回包含您指定之 Cmdlet 的角色的清單。

若要傳回包含您指定之 Cmdlet 的角色清單，請使用下列語法。

    Get-ManagementRole -Cmdlet <cmdlet>

此範例會傳回包含 **New-Mailbox** Cmdlet 的角色清單。

    Get-ManagementRole -Cmdlet New-Mailbox

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351125\(v=exchg.150\))。

## 列出包含特定參數的管理角色

您可以傳回包含一或多個指定的參數使用*CmdletParameters*參數**Get-ManagementRole**指令程式上的角色的清單。會傳回包含所有您指定的參數的唯一角色。

當您使用*CmdletParameters*參數時，您可以選擇加入*Cmdlet*參數。如果您納入*Cmdlet*參數，會傳回包含指定指令程式在您指定的參數的唯一角色。如果您未包含在*Cmdlet*參數包含您指定的參數的角色指令程式不論它們，所傳回。

若要傳回包含您指定之參數的角色清單，請使用下列語法。

    Get-ManagementRole [-Cmdlet <cmdlet>] -CmdletParameters <parameter 1>, <parameter 2...>

此範例會傳回包含 *Database* 和 *Server* 參數的角色清單 (不論它們存在於哪個 Cmdlet 上)。

    Get-ManagementRole -CmdletParameters Database, Server

此範例會傳回 *EmailAddresses* 參數僅存在於 **Set-Mailbox** Cmdlet 上的角色清單。

    Get-ManagementRole -Cmdlet Set-Mailbox -CmdletParameters EmailAddresses

您也可以使用萬用字元 (\*) 搭配 *Cmdlet* 或 *CmdletParameters* 參數來比對部分 Cmdlet 或參數名稱。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351125\(v=exchg.150\))。

## 列出特定角色類型的管理角色

您可以透過在 **Get-ManagementRole** Cmdlet 上使用 *RoleType* 參數來傳回以指定角色類型為基礎的角色清單。

若要傳回符合您指定之角色類型的角色清單，請使用下列語法。

    Get-ManagementRole -RoleType <roletype>

此範例會傳回以 `UmMailboxes` 角色類型為基礎的角色清單。

    Get-ManagementRole -RoleType UmMailboxes

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351125\(v=exchg.150\))。

## 列出上層角色的直接子項角色

您可以傳回**Get-ManagementRole**指令程式上使用*GetChildren*參數所指定的父系角色的直接子系角色的清單。會傳回包含您指定作為父系角色的角色的角色。

若要傳回上層角色之直接子項角色的清單，請使用以下語法。

    Get-ManagementRole <parent role name> -GetChildren

此範例會傳回 Disaster Recovery 角色之直接子項的清單。

    Get-ManagementRole "Disaster Recovery" -GetChildren

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351125\(v=exchg.150\))。

## 列出上層角色下的所有子項角色

您可以回到整個鏈結中的角色清單從指定之的上層角色的最後一個子角色**Get-ManagementRole**指令程式上使用*Recurse*參數。*Recurse*參數會指示**Get-ManagementRole**指令程式透過都會直到它達到的最後一個子角色每一個父項及子項關係遞迴向下。會傳回清單中包含父系角色。

此範例會傳回上層角色的所有子項角色清單。

    Get-ManagementRole <parent role name> -Recurse

此範例會傳回 Mail Recipients 角色的所有子項角色。

    Get-ManagementRole "Mail Recipients" -Recurse

如需詳細的語法及參數資訊，請參閱 [Get-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd351125\(v=exchg.150\))。

