---
title: '檢視角色範圍: Exchange 2013 Help'
TOCTitle: 檢視角色範圍
ms:assetid: 0bb3a434-6651-473a-94eb-4eb9a34e6f70
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335084(v=EXCHG.150)
ms:contentKeyID: 50472534
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視角色範圍

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

管理角色範圍決定哪些物件可提供使用給使用者以便可變更物件使用的指令程式和指派給他們的參數。您可以檢視來判斷哪些範圍已經新增至您的組織的範圍，設定為特定的範圍或項目範圍的孤立。

如需 Microsoft Exchange Server 2013 中管理角色範圍的相關資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

要尋找與角色範圍相關的其他管理工作嗎？取出[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理範圍」項目。

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

## 檢視特定範圍

您可以將 **Get-ManagementScope** Cmdlet 的輸出以管線傳送至 **Format-List** Cmdlet，以檢視範圍的詳細資料。

若要檢視特定範圍的詳細資料，請使用下列語法。

    Get-ManagementScope <scope name> | Format-List

此範例會擷取「西雅圖伺服器」範圍的詳細資料。

    Get-ManagementScope "Seattle Servers" | Format-List

如需詳細的語法及參數資訊，請參閱 [Get-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd298180\(v=exchg.150\))。

## 列出所有範圍

此範例會擷取您組織中範圍的清單。

    Get-ManagementScope

此指令程式會擷取獨佔和定期範圍。如果您只想要傳回獨佔範圍或一般範圍，請參閱"List 所有獨佔或一般範圍只"在本主題後面。

如需詳細的語法及參數資訊，請參閱 [Get-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd298180\(v=exchg.150\))。

## 列出所有孤立的範圍

*「孤立範圍」*是尚未與任何管理角色指派關聯的範圍。

此範例會擷取孤立範圍的清單。

    Get-ManagementScope -Orphan

如需詳細的語法及參數資訊，請參閱 [Get-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd298180\(v=exchg.150\))。

## 僅列出所有獨佔或一般領域

根據預設， **Get-ManagementScope**指令程式會傳回包含獨佔和定期範圍範圍的清單。如果您想要只傳回獨佔範圍或規則的範圍會使用下列語法。

    Get-ManagementScope -Exclusive < $true | $false >

此範例只會傳回獨佔範圍。

    Get-ManagementScope -Exclusive $true

此範例只會傳回一般範圍的清單。

    Get-ManagementScope -Exclusive $false

如需詳細的語法及參數資訊，請參閱 [Get-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd298180\(v=exchg.150\))。

