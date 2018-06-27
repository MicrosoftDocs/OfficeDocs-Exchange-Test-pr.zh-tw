---
title: '伺服器健康狀況與效能的權限: Exchange 2013 Help'
TOCTitle: 伺服器健康狀況與效能的權限
ms:assetid: 00b23fd3-6679-4b06-a3d4-51df3112b9cd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150479(v=EXCHG.150)
ms:contentKeyID: 50472448
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 伺服器健康狀況與效能的權限

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

執行設定 Microsoft Exchange Server 2013 各種元件之工作所需的權限，視正在執行的程序或要執行的 Cmdlet 而定。請參閱本主題中的每個章節，以取得其各自功能的詳細資訊。

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

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>某些功能可能會要求您在要管理的伺服器上具備本機系統管理員權限。若要管理這些功能，您必須是該伺服器上本機系統管理員群組的成員。</td>
</tr>
</tbody>
</table>


## Exchange 工作負載管理權限

下表列出執行管理的狀況及效能Exchange 2013組織的工作所需的權限。如需詳細資訊，請參閱[Exchange 工作負載管理](exchange-workload-management-exchange-2013-help.md)。

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
<td><p>使用者節流</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 工作負載節流設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
</tbody>
</table>


## Exchange 事件記錄檔權限

下表列出執行管理 Exchange 事件記錄檔設定的工作所需的權限。

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
<td><p>Exchange 事件記錄檔管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
</tbody>
</table>

