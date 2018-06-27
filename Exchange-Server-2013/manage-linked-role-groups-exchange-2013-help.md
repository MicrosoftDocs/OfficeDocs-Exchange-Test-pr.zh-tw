---
title: '管理連結的角色群組: Exchange 2013 Help'
TOCTitle: 管理連結的角色群組
ms:assetid: e2a07395-90c2-4d62-b15d-ac3ff28fe786
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657502(v=EXCHG.150)
ms:contentKeyID: 50474460
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理連結的角色群組

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-09_

您可以使用連結的管理角色群組讓管理 Microsoft Exchange Server 2013組織資源Active Directory樹系中的萬用安全性群組 (USG) 外部Active Directory樹系中的成員。關聯連結的角色群組中的外部樹系中的 USG，該成員 USG 都會授與管理角色指派給連結的角色群組所提供的權限。如需詳細資訊連結的角色群組的詳細資訊，請參閱[了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)。

若要建立及設定連結的角色群組，您需要使用**New-RoleGroup**和**Set-RoleGroup** cmdlet。如需詳細的語法及參數資訊，請參閱下列主題：

  - [New-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638181\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638182\(v=exchg.150\))

若欲瞭解更多與角色群組相關的管理工作，請參閱 [權限](permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成每項程序預估時間： 5 到 10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色群組」項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來建立或設定連結的角色群組。您必須使用 Exchange 管理命令介面。

  - 在最低限度下，設定連結的角色群組需要在其中將會位於連結的角色群組、 資源Active Directory樹系和使用者或 Usg 的所在位置的外部Active Directory樹系之間會建立單向信任。資源樹系必須信任外部樹系。

  - 您必須具有下列關於外部 Active Directory 樹系的資訊：
    
      - **認證**  您必須具有的使用者名稱和可以存取外部Active Directory樹系的密碼。此資訊是*LinkedCredential*參數的**New-RoleGroup**和**Set-RoleGroup**指令程式一起使用。
    
      - **網域控制站**  您必須外部Active Directory樹系中Active Directory網域控制站的完整的網域名稱 (FQDN)。此資訊是*LinkedDomainController*參數的**New-RoleGroup**和**Set-RoleGroup**指令程式一起使用。
    
      - **外部 USG**  您必須具備 USG 的完整名稱包含您想要連結的角色群組建立關聯的成員外部Active Directory樹系中。此資訊是**New-RoleGroup**和**Set-RoleGroup**指令程式上*LinkedForeignGroup*參數一起使用。

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

## 建立連結的角色群組

## 使用命令介面建立無範圍的連結角色群組

若要建立連結的角色群組並指派管理角色給該連結的角色群組，請執行下列動作：

1.  以變數儲存外部 Active Directory 樹系認證。
    
        $ForeignCredential = Get-Credential

2.  使用下列語法建立連結的角色群組。
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  使用外部 Active Directory 樹系中電腦上的 \[Active Directory 使用者和電腦\]，新增或移除外部 USG 的成員。

此範例會執行下列動作：

  - 擷取 users.contoso.com 外部Active Directory樹系的認證。這些認證用以連線至外部樹系中 DC01.users.contoso.com 網域控制站。

  - 在安裝 Exchange 2013 的資源樹系中建立名爲「符合性管理角色」的連結角色群組。

  - 將新角色群組連結到 users.contoso.com 外部 Active Directory 樹系中的符合性系統管理員 USG。

  - 將傳輸規則和日誌管理角色指派到新的連結角色群組。

<!-- end list -->

    $ForeignCredential = Get-Credential
    New-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles "Transport Rules", "Journaling"

## 使用命令介面建立具有自訂管理範圍的連結角色群組

您可以建立連結的角色群組與收件者的自訂管理範圍、 自訂設定管理範圍，或兩者。若要建立連結的角色群組及自訂範圍與管理角色指派給它，執行下列動作：

1.  以變數儲存外部 Active Directory 樹系認證。
    
        $ForeignCredential = Get-Credential

2.  使用下列語法建立連結的角色群組。
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -CustomConfigWriteScope <name of configuration scope> -CustomRecipientWriteScope <name of recipient scope> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  使用外部 Active Directory 樹系中電腦上的 \[Active Directory 使用者和電腦\]，新增或移除外部 USG 的成員。

此範例會執行下列動作：

  - 擷取 users.contoso.com 外部Active Directory樹系的認證。這些認證用以連線至外部樹系中 DC01.users.contoso.com 網域控制站。

  - 在安裝 Exchange 2013 的資源樹系中建立名爲「西雅圖符合性角色群組」的連結角色群組。

  - 將新角色群組連結到 users.contoso.com 外部 Active Directory 樹系中的西雅圖符合性系統管理員 USG。

  - 將傳輸規則和日誌管理角色指派給具有西雅圖收件者自訂收件者範圍的新連結角色群組。

<!-- end list -->

    $ForeignCredential = Get-Credential
    New-RoleGroup "Seattle Compliance Role Group" -LinkedForeignGroup "Seattle Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -CustomRecipientWriteScope "Seattle Recipients" -Roles "Transport Rules", "Journaling"

如需管理範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

## 使用命令介面建立具有 OU 範圍的連結角色群組

您可以建立使用 OU 收件者範圍的連結的角色群組。若要建立連結的角色群組和指派管理角色給它的 OU 範圍，執行下列動作：

1.  以變數儲存外部 Active Directory 樹系認證。
    
        $ForeignCredential = Get-Credential

2.  使用下列語法建立連結的角色群組。
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope <OU name> -Roles <role1, role2, role3...>

3.  使用外部 Active Directory 樹系中電腦上的 \[Active Directory 使用者和電腦\]，新增或移除外部 USG 的成員。

此範例會執行下列動作：

  - 擷取 users.contoso.com 外部Active Directory樹系的認證。這些認證用以連線至外部樹系中 DC01.users.contoso.com 網域控制站。

  - 在安裝 Exchange 2013 的資源樹系中建立名爲「主管符合性角色群組」的連結角色群組。

  - 將新角色群組連結到 users.contoso.com 外部 Active Directory 樹系中的主管符合性系統管理員 USG。

  - 將傳輸規則和日誌管理角色指派給具有 OU 收件者範圍主管 OU 的新連結角色群組。

<!-- end list -->

    $ForeignCredential = Get-Credential
    New-RoleGroup "Executives Compliance Role Group" -LinkedForeignGroup "Executives Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope "Executives OU" -Roles "Transport Rules", "Journaling"

如需管理範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

## 在連結的角色組上變更外部 USG

## 使用命令介面來變更連結的角色群組上的外部 USG

若要變更與連結的角色群組相關聯的外部 USG，請執行下列動作：

1.  以變數儲存外部 Active Directory 樹系認證。
    
        $ForeignCredential = Get-Credential

2.  使用下列語法在現有連結的角色群組上變更外部 USG。
    
        Set-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential 

此範例會執行下列動作：

  - 擷取 users.contoso.com 外部Active Directory樹系的認證。這些認證用以連線至外部樹系中 DC01.users.contoso.com 網域控制站。

  - 將 Compliance Role Group 角色群組上的外部 USG 變更為 Regulatory Compliance Officers。

<!-- end list -->

    $ForeignCredential = Get-Credential
    Set-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Regulatory Compliance Officers" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential

