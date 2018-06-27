---
title: '高可用性和站台回復性權限: Exchange 2013 Help'
TOCTitle: 高可用性和站台回復性權限
ms:assetid: 66085107-4d4d-41c3-a425-82314acd9eee
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638136(v=EXCHG.150)
ms:contentKeyID: 50473363
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 高可用性和站台回復性權限

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-11-12_

設定高可用性所需的權限而異正在執行的程序或您想要執行此指令程式。如需高可用性的詳細資訊，請參閱[高可用性和站台恢復](high-availability-and-site-resilience-exchange-2013-help.md)。

若要瞭解執行程序或執行 Cmdlet 所需的權限，請執行以下操作：

1.  在下表中，尋找與您想要執行的程序或 Cmdlet 最為相關的功能。

2.  接著查看功能所需的權限。您必須獲指派其中一個角色群組、相等的自訂角色群組，或相等的管理角色。您也可以按一下角色群組，查看其管理角色。如果功能列出多個角色群組，您只需要獲指派其中一個角色群組，就能使用功能。如需角色群組和管理角色的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  現在，執行 **Get-ManagementRoleAssignment** Cmdlet，查看指派給您的角色群組或管理角色，以瞭解您是否有管理該功能所需的權限。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須獲指派「角色管理」管理角色，才能執行 <strong>Get-ManagementRoleAssignment</strong> Cmdlet。如果您沒有執行 <strong>Get-ManagementRoleAssignment</strong> Cmdlet 的權限，請詢問您的 Exchange 系統管理員，以取得角色群組或是獲指派管理角色。</td>
    </tr>
    </tbody>
    </table>


如果您要將管理功能的能力委派給另一個使用者，請參閱[委派角色指派](delegate-role-assignments-exchange-2013-help.md)。

## 資料庫可用性群組權限

您可以使用下表中的功能來新增、移除及設定資料庫可用性群組 (DAG) 的設定。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>資料庫可用性群組成員格</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">資料庫可用性群組角色</a></p></td>
</tr>
<tr class="even">
<td><p>資料庫可用性群組內容</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">資料庫可用性群組角色</a></p></td>
</tr>
<tr class="odd">
<td><p>資料庫可用性群組</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">資料庫可用性群組角色</a></p></td>
</tr>
<tr class="even">
<td><p>資料庫可用性網路</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">資料庫可用性群組角色</a></p></td>
</tr>
</tbody>
</table>


## 信箱資料庫副本權限

您可以使用下表中的功能來新增、移除、更新及啟動信箱資料庫副本。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>必要的權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>資料庫轉換</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="databases-role-exchange-2013-help.md">資料庫角色</a></p></td>
</tr>
<tr class="even">
<td><p>信箱資料庫副本</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">資料庫副本的角色</a></p></td>
</tr>
<tr class="odd">
<td><p>伺服器轉換</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="databases-role-exchange-2013-help.md">資料庫角色</a></p></td>
</tr>
<tr class="even">
<td><p>更新信箱資料庫副本</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">資料庫副本的角色</a></p></td>
</tr>
</tbody>
</table>

