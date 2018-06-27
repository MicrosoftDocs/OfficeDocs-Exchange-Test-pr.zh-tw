---
title: '角色範圍變更: Exchange 2013 Help'
TOCTitle: 角色範圍變更
ms:assetid: 9180e1e0-c352-4ccd-8da6-885a2e309867
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298145(v=EXCHG.150)
ms:contentKeyID: 50473741
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 角色範圍變更

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

管理角色範圍決定哪些物件可提供使用給使用者以便可變更物件使用的指令程式和指派給他們的參數。變更範圍，您可以變更哪些物件會對可用來建立、 變更或移除使用者。

您可以變更的自訂管理範圍。您可以變更獨佔或一般範圍。如果您變更獨佔範圍時，新的範圍會立即生效。如果您想要變更與預先定義或組織單位 (OU) 」 管理範圍的管理角色指派，請參閱[變更角色指派](change-a-role-assignment-exchange-2013-help.md)。

如需 Microsoft Exchange Server 2013 中管理角色範圍和指派的相關資訊，請參閱下列主題：

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

要尋找與角色範圍相關的其他管理工作嗎？取出[進階權限](advanced-permissions-exchange-2013-help.md)。

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


## 您要執行的工作

## 變更範圍名稱

若要變更範圍的名稱，請使用下列語法。

    Set-ManagementScope <current scope name> -Name <new scope name>

此範例會將 Seattle Servers 範圍變更為 Seattle Exchange Servers。

    Set-ManagementScope "Seattle Servers" -Name "Seattle Exchange Servers"

如需詳細的語法及參數資訊，請參閱 [Set-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd297996\(v=exchg.150\))。

## 變更某個範圍上的收件者篩選

若要變更某個範圍的收件者篩選，請使用下列語法。

    Set-ManagementScope <scope name> -RecipientRestrictionFilter { <new recipient filter> }

此範例會變更收件者篩選，以符合 **Company** 內容設爲 contoso 的所有收件者物件。

    Set-ManagementScope "Company Scope" -RecipientRestrictionFilter { Company -eq 'contoso' }

如需詳細的語法及參數資訊，請參閱 [Set-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd297996\(v=exchg.150\))。

如需收件者篩選的詳細資訊，或若要查看可篩選收件者內容的清單，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

## 變更範圍上的組織單位根

若要變更範圍上的 OU 根，請使用下列語法。

    Set-ManagementScope <scope name> -RecipientRoot <OU>

此範例會將 contoso.com 網域下的 OU 根變更為 North America/Sales Sales Users OU。

    Set-ManagementScope "Sales Users" -RecipientRoot "contoso.com/North America/Sales"

如需詳細的語法及參數資訊，請參閱 [Set-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd297996\(v=exchg.150\))。

## 變更範圍上的伺服器篩選

若要變更某個範圍的伺服器篩選，請使用下列語法。

    Set-ManagementScope <scope name> -ServerRestrictionFilter { <new server filter> }

此範例會變更伺服器篩選器以比對所有 **ServerSite** 屬性設定為 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' 的伺服器物件。

    Set-ManagementScope "Company Scope" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

如需詳細的語法及參數資訊，請參閱 [Set-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd297996\(v=exchg.150\))。

如需伺服器篩選的詳細資訊，或若要查看可篩選伺服器內容的清單，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

## 變更範圍上的伺服器清單

您無法變更伺服器上的範圍的清單。如果您需要變更伺服器\] 清單中，您需要執行下列動作：

1.  如有需要，使用[檢視角色範圍](view-role-scopes-exchange-2013-help.md)主題中的「檢視特定範圍」程序，擷取範圍中要取代的目前伺服器清單。

2.  使用範圍建立新的伺服器清單 」 步驟 1： 建立自訂的範圍" [建立規則或獨佔範圍](create-a-regular-or-exclusive-scope-exchange-2013-help.md)主題中的程序。

3.  使用[變更角色指派](change-a-role-assignment-exchange-2013-help.md)主題中的「使用命令介面變更角色指派上的伺服器篩選或清單式範圍」程序，將使用舊範圍的所有管理角色指派變更為使用新範圍。

4.  使用[移除角色範圍](remove-a-role-scope-exchange-2013-help.md)主題中的程序移除舊範圍。

## 變更某個範圍上的資料庫篩選

若要變更某個範圍的資料庫篩選，請使用下列語法。

    Set-ManagementScope <scope name> -DatabaseRestrictionFilter { <new database filter> }

此範例會變更資料庫篩選，以符合 **Name** 內容包含字串「Executive」的所有資料庫物件。

    Set-ManagementScope "Database Executive Scope" -DatabaseRestrictionFilter { Name -Like "*Executive*" }

如需詳細的語法及參數資訊，請參閱 [Set-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd297996\(v=exchg.150\))。

如需資料庫篩選的詳細資訊，或若要查看可篩選資料庫內容的清單，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

## 變更某個範圍上的資料庫清單

您無法變更範圍上的資料庫的清單。如果您需要變更資料庫\] 清單中，您需要執行下列動作：

1.  如有需要，請使用[檢視角色範圍](view-role-scopes-exchange-2013-help.md)主題中的「檢視特定範圍」程序，擷取範圍中要取代的目前資料庫清單。

2.  使用範圍建立新的資料庫清單 」 步驟 1： 建立自訂的範圍" [建立規則或獨佔範圍](create-a-regular-or-exclusive-scope-exchange-2013-help.md)主題中的程序。

3.  使用[變更角色指派](change-a-role-assignment-exchange-2013-help.md)主題中的「使用命令介面變更角色指派上的資料庫篩選或清單式範圍」程序，將使用舊範圍的所有管理角色指派變更為使用新範圍。

4.  使用[移除角色範圍](remove-a-role-scope-exchange-2013-help.md)主題中的程序移除舊範圍。

