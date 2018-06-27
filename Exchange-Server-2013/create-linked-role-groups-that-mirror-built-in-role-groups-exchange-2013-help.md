---
title: '建立鏡像內建角色群組的連結的角色群組: Exchange 2013 Help'
TOCTitle: 建立鏡像內建角色群組的連結的角色群組
ms:assetid: 89dfcbb3-0568-4bbf-a885-746b91ba307e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876918(v=EXCHG.150)
ms:contentKeyID: 50473687
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立鏡像內建角色群組的連結的角色群組

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

使用連結的管理角色群組中的 Microsoft Exchange Server 2013，您可以在外部使用者樹系中連結Exchange 2013資源樹系中的角色群組與萬用安全性群組 (USG)。當您想要使用者樹系內擁有帳戶的系統管理員管理資源樹系中執行Exchange伺服器，這很有用。如需詳細資訊連結的角色群組的詳細資訊，請參閱[了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)。

根據預設， Exchange 2013包含以管理各種功能及工作的功能權限提供給您的內建角色群組的數目。每個角色群組被適合提供每個功能及工作函數的特定權限。不過，這些角色群組無法連結至外部樹系中 Usg。它們只可以包含使用者和 Usg 從本機資源樹系。幸運地是，則有可能複寫這些使用連結的角色群組的內建角色群組。

您可以重新建立每個內建角色群組做為連結的角色群組。所有管理角色及指派給每個角色群組的管理範圍會新增至新的連結的角色群組。如需管理角色和範圍的詳細資訊，請參閱下列主題：

  - [了解管理角色](understanding-management-roles-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

要尋找與角色群組相關的其他管理工作嗎？取出[權限](permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色群組」項目。

  - 您必須使用命令介面來執行這些程序。

  - 設定連結的角色群組需要資源Active Directory樹系中將會位於連結的角色群組，與外部Active Directory樹系的使用者或 Usg 的所在位置之間的單向信任。資源樹系必須信任外部樹系。

  - 您必須具有下列關於外部 Active Directory 樹系的資訊：
    
      - **認證**  您必須具有的使用者名稱和可以存取外部Active Directory樹系的密碼。此資訊是**New-RoleGroup**指令程式上*LinkedCredential*參數一起使用。此資訊是執行**Get-Credential**指令程式來取得。使用者名稱的格式是*domain*\\*username*。
    
      - **網域控制站**  您必須外部Active Directory樹系中Active Directory網域控制站的完整的網域名稱 (FQDN)。此資訊是**New-RoleGroup**指令程式上*LinkedDomainController*參數一起使用。
    
      - **外部 USG**  您必須具備 USG 的完整名稱包含您想要連結的角色群組建立關聯的成員外部Active Directory樹系中。此資訊是**New-RoleGroup**指令程式上*LinkedForeignGroup*參數一起使用。

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


## 使用命令介面可建立複寫內建角色群組的連結角色群組

下列各節說明如何重新建立做為連結的角色群組的每個角色群組。完成重新建立所有為連結的角色群組的內建角色群組的每一節中的程序。

## 建立組織管理的連結角色群組

若要重新建立連結的角色群組的形式組織管理角色群組，您可以執行不同於用來重新建立其他的內建角色群組的程序的程序。這是因為組織管理角色群組不具委派與所有管理角色之間的角色指派。重新建立委派角色指派需要額外的步驟。

1.  建立要連結至 組織管理 角色群組的外部樹系 USG。

2.  以變數儲存外部 Active Directory 樹系認證。
    
        $ForeignCredential = Get-Credential

3.  透過變數儲存指派至 組織管理 角色群組的所有角色。
    
        $OrgMgmt  = Get-RoleGroup "Organization Management"

4.  建立 組織管理 連結角色群組，並新增指派至內建 組織管理 角色群組的角色。
    
        New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles

5.  移除新 組織管理 連結角色群組及 My\* 一般使用者角色之間的所有一般指派。
    
        Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment

6.  新增新 組織管理 連結角色群組及所有管理角色間的委派角色指派。
    
        Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

此範例假設下列值用於每個參數：

  - **LinkedForeignGroup**   `Organization Management Administrators`

  - **LinkedDomainController**   `DC01.users.contoso.com`

此範例使用前值來將 組織管理 角色群組重新建立為連結角色群組。

    $ForeignCredential = Get-Credential
    $OrgMgmt  = Get-RoleGroup "Organization Management"
    New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup "Organization Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
    Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
    Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

## 建立所有其他連結的角色群組

若要將內建角色群組 (除了 組織管理 角色群組以外) 重新建立為連結的角色群組，請對每個群組執行以下程序。

1.  爲每個角色群組建立連結至每個新角色群組的外部樹系 USG。

2.  儲存在變數中的外部Active Directory樹系認證。您只需要一次執行這項作業。
    
        $ForeignCredential = Get-Credential

3.  擷取使用下列 Cmdlet 的角色群組清單。
    
        Get-RoleGroup

4.  針對 組織管理 角色群組以外的每個角色群組，請執行下列作業。
    
        $RoleGroup = Get-RoleGroup <name of role group to re-create>
        New-RoleGroup "<role group name> - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

5.  針對想重新建立為連結角色群組的每個內建角色群組，重複先前步驟。

此範例假設下列值用於每個參數：

  - **LinkedDomainController**   `DC01.users.contoso.com`

  - **要重新建立為連結角色群組的內建角色群組**   `Recipient Management, Server Management`

  - **收件者管理連結角色群組的外部群組**   `Recipient Management Administrators`

  - **伺服器管理連結角色群組的外部群組**   `Server Management Administrators`

此範例使用前值來將 收件者管理 及「伺服器管理」角色群組重新建立為連結角色群組。

    $ForeignCredential = Get-Credential
    Get-RoleGroup
    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Recipient Management - Linked" -LinkedForeignGroup "Recipient Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
    $RoleGroup = Get-RoleGroup "Server Management"
    New-RoleGroup "Server Management - Linked" -LinkedForeignGroup "Server Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

## 其他工作

在建立連結角色群組之後，您可能還想要：

新增成員到外部樹系中使用 Active Directory 使用者及電腦的外部 USG。

移除內建角色群組的成員。如需詳細資訊，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

新增、 移除或變更角色上的新連結的角色群組的範圍。如需詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

建立其他連結的角色群組。如需詳細資訊，請參閱[管理連結的角色群組](manage-linked-role-groups-exchange-2013-help.md)。

