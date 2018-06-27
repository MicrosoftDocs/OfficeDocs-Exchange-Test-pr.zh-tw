---
title: '建立規則或獨佔範圍: Exchange 2013 Help'
TOCTitle: 建立規則或獨佔範圍
ms:assetid: b97a5be3-15cc-4954-ba30-a824a95e21be
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351083(v=EXCHG.150)
ms:contentKeyID: 50474048
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立規則或獨佔範圍

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

管理角色範圍決定哪些物件可提供使用給使用者以便可變更物件使用的指令程式和指派給他們的參數。新增的管理範圍，您可以讓使用者可以管理特定伺服器、 資料庫、 收件者\] 和其他物件時要變更其他物件限制在組織中的設定管理角色指派。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您建立的規則或獨佔範圍時，您覆寫您要指派的管理角色定義寫入範圍。您不能覆寫已在 「 管理 」 角色的讀取的範圍。</td>
</tr>
</tbody>
</table>


您可以建立自訂管理範圍和新增或變更的管理角色指派。如果您想要使用預先建立或組織單位 (OU) 」 管理範圍建立管理角色指派，請參閱[將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)。

如需 Microsoft Exchange Server 2013 中管理角色範圍和指派的相關資訊，請參閱下列主題：

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

要尋找與範圍相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理範圍」項目。

  - 您必須使用命令介面來執行這些程序。

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


## 該怎麼做？

## 步驟 1： 建立自訂範圍

若要建立自訂範圍，請選擇下列其中一種範圍類型。

## 收件者篩選器範圍

使用*RecipientRestrictionFilter*參數在**New-ManagementScope**指令程式可建立收件者篩選器為基礎的範圍。當您建立收件者篩選，除了收件者的屬性篩選，您可以指定執行篩選查詢的 OU。當您指定的基底的 OU 時，進一步會限制寫入範圍的角色。

如需管理範圍篩選的相關資訊，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

使用下列語法，能以基本 OU 來建立網域限制篩選器範圍。

    New-ManagementScope -Name <scope name> -RecipientRestrictionFilter <filter query> [-RecipientRoot <OU>]

此範例會建立包含 contoso.com/Sales OU 中所有信箱的範圍。

    New-ManagementScope -Name "Mailboxes in Sales OU" -RecipientRestrictionFilter { RecipientType -eq 'UserMailbox' } -RecipientRoot "contoso.com/Sales OU"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您希望篩選器套用到管理角色整個隱含的讀取範圍，而不是只套用到特定 OU 中，您可以省略 <em>RecipientRoot</em> 參數。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [New-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd335137\(v=exchg.150\))。

## 伺服器篩選器組態範圍

使用*ServerRestrictionFilter*參數在**New-ManagementScope**指令程式可建立伺服器篩選器型組態範圍。伺服器篩選可讓您建立僅適用於伺服器符合您指定此篩選條件的範圍。

如需管理範圍篩選條件的詳細資訊，以及可篩選的伺服器內容的清單，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

使用下列語法，可建立伺服器篩選器範圍。

    New-ManagementScope -Name <scope name> -ServerRestrictionFilter <filter query>

此範例會建立包含 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' AD (Active Directory) 站台內所有伺服器的範圍。

    New-ManagementScope -Name "Servers in Seattle AD site" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

如需詳細的語法及參數資訊，請參閱 [New-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd335137\(v=exchg.150\))。

## 伺服器清單組態範圍

使用*ServerList*參數在**New-ManagementScope**指令程式可建立伺服器清單型組態範圍。伺服器清單範圍可讓您建立僅適用於您在清單中指定之伺服器的範圍。

使用下列語法，可建立伺服器清單範圍。

    New-ManagementScope -Name <scope name> -ServerList <server 1>, <server 2...>

此範例會建立僅套用至 MBX1、MBX3 與 MBX5 的範圍。

    New-ManagementScope -Name "Mailbox servers" -ServerList MBX1,MBX3,MBX5

如需詳細的語法及參數資訊，請參閱 [New-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd335137\(v=exchg.150\))。

## 資料庫篩選器組態範圍

使用*DatabaseRestrictionFilter*參數在**New-ManagementScope**指令程式可建立資料庫篩選器型組態範圍。資料庫篩選器可讓您建立僅適用於資料庫符合您指定此篩選條件的範圍。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>資料庫範圍與相關聯的角色指派只適用於連線到執行 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 的伺服器的使用者或更新版本或Exchange 2013。如果指派資料庫範圍與相關聯的角色指派的使用者連線至預先Exchange 2010 SP1 的伺服器、 角色指派不會套用至該使用者，並不會授與使用者角色指派所提供的任何權限。</td>
</tr>
</tbody>
</table>


如需管理範圍篩選器的詳細資訊，以及可篩選之資料庫內容的清單，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

使用下列語法，可建立資料庫限制篩選器。

    New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>

這個範例會建立一個範圍，而此範圍包括資料庫 **Name** 屬性中包含 "Executive" 字串的所有資料庫。

    New-ManagementScope -Name "Executive Databases" -DatabaseRestrictionFilter { Name -Like '*Executive*' }

如需詳細的語法及參數資訊，請參閱 [New-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd335137\(v=exchg.150\))。

## 資料庫清單組態範圍

使用*DatabaseList*參數在**New-ManagementScope**指令程式可建立資料庫\] 清單為基礎的組態範圍。資料庫清單範圍可讓您建立僅適用於您在清單中指定之資料庫的範圍。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>資料庫範圍與相關聯的角色指派只適用於連線到執行 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 的伺服器的使用者或更新版本或Exchange 2013。如果指派資料庫範圍與相關聯的角色指派的使用者連線至預先Exchange 2010 SP1 的伺服器、 角色指派不會套用至該使用者，並不會授與使用者角色指派所提供的任何權限。</td>
</tr>
</tbody>
</table>


使用下列語法，可建立資料庫清單範圍。

    New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>

這個範例會建立只套用至資料庫 Database 1、Database 2 和 Database 3 的範圍。

    New-ManagementScope -Name "Primary databases" -DatabaseList "Database 1", "Database 2", "Database 3"

如需詳細的語法及參數資訊，請參閱 [New-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd335137\(v=exchg.150\))。

## 獨佔範圍

使用**New-ManagementScope**指令程式所建立的任何範圍可以指定為獨佔範圍。若要建立獨佔範圍，您使用同一個命令中其中一個以上的區段建立收件者篩選器型範圍、 伺服器篩選器型範圍、 伺服器清單型範圍、 資料庫篩選器型範圍或資料庫清單型範圍並再將*Exclusive*參數新增至命令。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您建立獨佔管理範圍時，只指派獨佔範圍包含要修改的物件的角色 assignees 可以存取這些物件。僅在以獨佔範圍的角色指派的管理員可以存取這些獨佔或受保護，物件。</td>
</tr>
</tbody>
</table>


此範例會建立符合 Executives 部門中任何使用者的獨佔收件者篩選器式範圍。

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive

根據預設，建立獨佔範圍之後，您正在需要確認您建立獨佔範圍和您知道獨佔範圍對未獨佔的現有角色指派的影響。如果您想要隱藏警告中，您可以使用*Force*參數。此範例會建立同一個範圍上一個範例中，但不包含一則警告訊息。

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive -Force

如需詳細的語法及參數資訊，請參閱 [New-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd335137\(v=exchg.150\))。

## 步驟 2： 新增或變更的管理角色指派

在您建立範圍之後，必須將其新增至新的或現有的管理角色指派。

如果您建立一個管理範圍，並想將其新增到您將即將建立的新管理角色指派，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

如果您建立一個管理角色範圍，並想將其新增到現有的管理角色指派，請參閱下列主題：

  - [管理角色指派原則](manage-role-assignment-policies-exchange-2013-help.md)

  - [變更角色指派](change-a-role-assignment-exchange-2013-help.md)

