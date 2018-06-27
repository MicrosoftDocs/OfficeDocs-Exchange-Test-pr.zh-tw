---
title: '郵件原則及符合性權限: Exchange 2013 Help'
TOCTitle: 郵件原則及符合性權限
ms:assetid: ec4d3b9f-b85a-4cb9-95f5-6fc149c3899b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638205(v=EXCHG.150)
ms:contentKeyID: 50474532
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 郵件原則及符合性權限

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

設定郵件原則及符合性時，所需的權限視要執行的程序或您想執行的指令程式而有所不同。如需訊息原則及符合性的相關資訊，請參閱[郵件原則及符合性](messaging-policy-and-compliance-exchange-2013-help.md)。

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


## 郵件原則及符合性權限

您可以使用下表中的功能來設定訊息原則與符合性功能。此表會列出設定每個功能所需的角色群組。

獲指派僅檢視管理角色群組的使用者，可以檢視下表中功能的組態。如需相關資訊，請參閱[僅限檢視組織管理](view-only-organization-management-exchange-2013-help.md)。


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
<td><p>防止資料遺失 (DLP)</p></td>
<td><p>如果使用 Office 365：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 全域管理員</a>，這會自動包含 Exchange <a href="organization-management-exchange-2013-help.md">組織管理</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 服務管理員</a>，加上 Exchange 中<a href="organization-management-exchange-2013-help.md">組織管理</a>系統管理員角色群組</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 密碼管理</a></p></li>
</ul>
<p>如果只使用 Exchange Server 2013 或 Exchange Online：</p>
<ul>
<li><p><a href="compliance-management-exchange-2013-help.md">規範管理</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>刪除信箱內容 (使用 <a href="https://technet.microsoft.com/zh-tw/library/dd298173(v=exchg.150)">Search-Mailbox</a> 指令程式搭配 <em>DeleteContent</em> 參數)</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">探索管理</a> <strong>與</strong></p>
<p><a href="mailbox-import-export-role-exchange-2013-help.md">信箱匯入匯出角色</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，「信箱匯入匯出」角色並未指派給任何角色群組。您可以指派管理角色給內建或自訂的角色群組、使用者或萬用安全性群組。建議將角色指派給角色群組。如需詳細資訊，請參閱<a href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">將角色新增至使用者或 USG</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>探索信箱 - 建立</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>日誌</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="odd">
<td><p>信箱稽核記錄</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="even">
<td><p>郵件分類</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>通訊記錄管理</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">規範管理</a></p>
<p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="even">
<td><p>原有範圍 eDiscovery</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">探索管理</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，探索管理角色群組沒有任何成員。沒有使用者 (包括系統管理員) 擁有搜尋信箱的必要權限。如需詳細資訊，請參閱<a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Exchange 中指派 eDiscovery 權限</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>原有範圍暫止</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">探索管理</a></p>
<p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要建立查詢式「就地保留」，使用者需要獲得直接指派「信箱搜尋」和「訴訟資料暫留」角色，或是透過獲指派這兩個角色之角色群組的成員資格取得。若不要使用查詢而建立「就地保留」(如此會將所有信箱項目都保留)，您必須獲指派「訴訟資料暫留」角色。「探索管理」角色群組即獲指派這兩個角色。<br />
「組織管理」角色群組則獲指派「訴訟資料暫留」角色。「組織管理」角色群組的成員可對信箱中的所有項目進行「就地保留」，但不能建立查詢式「就地保留」。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>就地封存</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>就地封存 — 測試連線</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>資訊版權管理 (IRM) 組態</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">規範管理</a></p>
<p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>保留原則 - 套用</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="even">
<td><p>保留原則 - 建立</p></td>
<td><p>請參閱「郵件記錄管理」項目</p></td>
</tr>
<tr class="odd">
<td><p>傳輸規則</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
</tbody>
</table>

