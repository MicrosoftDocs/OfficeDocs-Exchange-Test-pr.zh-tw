---
title: '郵件流程權限: Exchange 2013 Help'
TOCTitle: 郵件流程權限
ms:assetid: f49f4fb5-af75-43cb-900f-c5f7b8cfa143
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638213(v=EXCHG.150)
ms:contentKeyID: 50474597
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 郵件流程權限

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

執行與郵件流程相關之工作所需的權限，因所執行的程序或您要執行的 Cmdlet 而異。如需傳輸功能的相關資訊，請參閱 [郵件流程](mail-flow-exchange-2013-help.md)。

本主題將列出管理 Microsoft Exchange Server 2013的郵件流程功能所需的權限。如需 Office 365 的權限與 Exchange 權限的方式，查看[Office 365 中的權限](https://go.microsoft.com/fwlink/p/?linkid=335814)。

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
<td>您要管理的某些功能可能存在於 Edge Transport server 上。若要管理 Edge Transport server 上的功能，您必須在要管理的 Edge Transport server 上是本機系統管理員群組的成員。Edge Transport server 不會使用角色型存取控制 (RBAC)。在下表中，可以在 Edge Transport server 上管理的功能會於 [需要的權限] 欄中顯示「邊際傳輸本機系統管理員」。</td>
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
<td>某些功能可能會要求您在要管理的伺服器上具備本機系統管理員權限。若要管理這些功能，您必須是該伺服器上本機系統管理員群組的成員。</td>
</tr>
</tbody>
</table>


## 郵件流程權限

您可以使用下表中的功能，來設定用戶端存取伺服器上的前端傳輸服務、信箱伺服器上的傳輸服務、信箱伺服器上的信箱傳輸服務以及信箱伺服器上的信箱傳輸服務之郵件流程設定值。列出設定每個功能所需的權限。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中顯示的功能的組態。如需詳細資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。

**信箱伺服器和用戶端存取伺服器**


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
<td><p>公認的網域</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>Active Directory 站台與站台連結管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>反垃圾郵件功能</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
</tr>
<tr class="even">
<td><p>反垃圾郵件更新</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
</tr>
<tr class="odd">
<td><p>憑證管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>傳遞代理程式連接器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>DSN</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>EdgeSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>外部連接器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>Front End Transport 服務</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
</tr>
<tr class="odd">
<td><p>日誌</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="even">
<td><p>信箱存取</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>信箱垃圾郵件組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="even">
<td><p>Mailbox Transport 服務</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
</tr>
<tr class="odd">
<td><p>MailTips</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>郵件分類</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="odd">
<td><p>郵件追蹤</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>已仲裁的傳輸</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>佇列</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>接收連接器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
</tr>
<tr class="odd">
<td><p>遠端網域</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>安全清單彙總</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="odd">
<td><p>傳送連接器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>陰影備援</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>測試郵件流量</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>測試傳輸規則處理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>傳輸代理程式</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="even">
<td><p>傳輸組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>傳輸記錄檔</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>傳輸規則</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Transport 服務</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
</tr>
<tr class="even">
<td><p>X.400 網域</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
</tbody>
</table>


**Edge Transport Server**


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
<td><p>公認網域 - 邊緣傳輸</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
<tr class="even">
<td><p>地址修正 - Edge Transport</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
<tr class="odd">
<td><p>Edge Transport server</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
<tr class="even">
<td><p>EdgeSync - 邊緣傳輸</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
<tr class="odd">
<td><p>佇列 - 邊緣傳輸</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
<tr class="even">
<td><p>接收連接器 - 邊緣傳輸</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
<tr class="odd">
<td><p>傳送連接器 - 邊緣傳輸</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
<tr class="even">
<td><p>傳輸組態 - 邊緣傳輸</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
<tr class="odd">
<td><p>傳輸記錄檔 - 邊緣傳輸</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
<tr class="even">
<td><p>傳輸規則 - 邊緣傳輸</p></td>
<td><p>邊際傳輸本機管理員</p></td>
</tr>
</tbody>
</table>

