---
title: '收件者權限: Exchange 2013 Help'
TOCTitle: 收件者權限
ms:assetid: 5b690bcb-c6df-4511-90e1-08ca91f43b37
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638132(v=EXCHG.150)
ms:contentKeyID: 50473265
ms.date: 01/19/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 收件者權限

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

執行工作以管理收件者所需的權限，因所執行的程序或您要執行的指令程式而異。

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

## 信箱伺服器權限

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
<td><p>行事曆修復、伺服器組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>委派信箱伺服器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>電子郵件地址原則</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 搜尋</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 搜尋 – 診斷</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p>
<p>支援診斷角色</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>支援診斷角色不指派給角色群組。如需詳細資訊，請參閱<a href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">將角色新增至使用者或 USG</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>群組度量資訊</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>匯入匯出</p></td>
<td><p>信箱匯入匯出角色</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>信箱匯入匯出角色不指派給角色群組。如需詳細資訊，請參閱<a href="mailbox-import-export-role-exchange-2013-help.md">信箱匯入匯出角色</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>信箱助理員</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>信箱移動</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>信箱復原</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>信箱修復要求</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>信箱還原要求</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>信箱伺服器組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>管理信箱伺服器上的 Exchange Search Indexer</p></td>
<td><p>信箱伺服器上的本機系統管理員</p></td>
</tr>
<tr class="odd">
<td><p>MAPI 連線</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="even">
<td><p>OAB 虛擬目錄</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>移除儲存區信箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
</tbody>
</table>


## 行事曆與共用權限

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
<td><p>行事曆組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="even">
<td><p>行事曆診斷</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p>
<p><a href="compliance-management-exchange-2013-help.md">規範管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="odd">
<td><p>行事曆處理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="even">
<td><p>通知</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>組織關係</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>共用原則</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
</tbody>
</table>


## 資源信箱組態權限

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
<td><p>預約原則</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="even">
<td><p>委派</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>資源信箱結構描述組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
</tbody>
</table>


## 信箱資料庫權限

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
<td><p>信箱資料庫</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
</tbody>
</table>


## 收件者佈建權限

此表格包含管理收件者所需的各種權限。

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
<td><p>通訊清單、GAL</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>反垃圾郵件</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>適用於 Outlook 的應用程式</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="even">
<td><p>套用共用原則</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>仲裁</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>封存連線</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>指派離線通訊錄</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>自動回覆</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="odd">
<td><p>行事曆組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>行事曆修復</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>聯絡人彙總設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>中斷連線的信箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="odd">
<td><p>通訊群組</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>動態通訊群組</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>電子郵件地址</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
<tr class="even">
<td><p>收件匣規則</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="odd">
<td><p>郵件連絡人</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>郵件提示</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>郵件使用者</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>信箱資料夾權限</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="odd">
<td><p>信箱資料夾</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>MAPI 連線</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>郵件組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="even">
<td><p>郵件配額</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>仲裁</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>權限和委派</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>封存信箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>收件者資料內容</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>遠端信箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>保留和合法持有</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
</tr>
<tr class="odd">
<td><p>以下列傳送</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>拼字組態</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
<tr class="odd">
<td><p>整合通訊</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
<tr class="even">
<td><p>使用者信箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>使用者相片</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
</tr>
</tbody>
</table>


## 信箱移動與遷移權限

表格包含移動內部部署信箱至不同網域或樹系、以及遷移內部部署信箱至雲端組織/由雲端組織遷移所需的權限。


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
<td><p>信箱移動 （本機或跨樹系）</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p>信箱移動 （混合部署）</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="odd">
<td><p>遷移 (自雲端上線或離線遷移)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
</tbody>
</table>

