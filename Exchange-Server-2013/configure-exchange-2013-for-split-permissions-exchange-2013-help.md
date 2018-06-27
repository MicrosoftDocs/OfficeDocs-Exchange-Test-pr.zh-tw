---
title: '設定 Exchange 2013 分割權限: Exchange 2013 Help'
TOCTitle: 設定 Exchange 2013 分割權限
ms:assetid: 8c74f893-a6f3-4869-8571-3bc0f662cc87
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638155(v=EXCHG.150)
ms:contentKeyID: 50473662
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Exchange 2013 分割權限

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

分割權限可讓兩個不同的群組 (例如 Active Directory Administrators 和 Microsoft Exchange Server 2013 Administrators) 管理各自的服務、物件和屬性。Active Directory Administrators 管理安全性主體 (例如使用者)，提供存取 Active Directory 樹系的權限。Exchange Administrators 管理 Active Directory 物件上與 Exchange 相關的屬性，以及建立和管理 Exchange 特定的物件。

Microsoft Exchange Server 2013 提供了下列類型的分割權限模型：

  - **RBAC 分割權限**  Active Directory網域分割區中建立安全性主體的權限所控制的角色存取控制 (RBAC)。只是屬於適當的角色群組的成員可以建立安全性主體。

  - **Active Directory 分割權限**  從任何Exchange使用者、 服務或伺服器完全移除Active Directory網域分割區中建立安全性主體的權限。建立安全性主體的 RBAC 不提供的任何選項。使用Active Directory管理工具必須執行Active Directory中的安全性主體的建立。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Active Directory 可在執行 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更新版、Exchange 2013 或兩個版本的 Exchange 之組織中使用。</td>
    </tr>
    </tbody>
    </table>


您選擇的模型結構和組織的需求而定。選擇的程序可適用於您想要設定的模型。我們建議您使用的 RBAC 分割權限模型。RBAC 分割權限模型可大幅更彈性地同時為Active Directory分割權限提供相同的管理分離。

如需共用與分割權限的相關資訊，請參閱[了解分割權限](understanding-split-permissions-exchange-2013-help.md)。

如需管理角色群組、管理角色以及一般與委派管理角色指派的相關資訊，請參閱下列主題：

  - [了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)

  - [了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)

  - [了解管理角色](understanding-management-roles-exchange-2013-help.md)

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

要尋找相關的權限的其他管理工作嗎？取出[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「Active Directory 分割權限」項目。

  - 您必須使用 Windows PowerShell、 Windows 命令介面中，或兩者，才能執行這些程序。如需詳細資訊，請參閱每項程序。

  - 如果您在組織中有Exchange 2010伺服器，您所選取的權限模型也會套用至這些伺服器。

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

## 切換至 RBAC 分割權限

您可以設定Exchange 2013組織 rbac 分割權限。當您已完成時，只有Active Directory系統管理員將能夠建立Active Directory安全性主體。這表示Exchange系統管理員將不能夠使用下列 cmdlet：

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Exchange系統管理員將只能夠管理現有的Active Directory安全性主體的Exchange屬性。不過，他們將能夠建立及管理Exchange-傳輸規則及通訊群組之類的特定物件。如需詳細資訊，請參閱 ＜ [了解分割權限](understanding-split-permissions-exchange-2013-help.md)"RBAC 分割權限 」 一節。

若要設定Exchange 2013分割權限，您必須將建立郵件收件者角色與安全性群組建立與成員資格角色指派給角色群組包含Active Directory系統管理員的成員。然後您必須移除這些角色與任何角色群組或萬用安全性群組 (USG)，其中包含Exchange管理員之間的工作分派。

若要設定 RBAC 分割權限，請執行下列動作：

1.  如果目前將組織設定為實作 Active Directory 分割權限，請從 Windows 命令介面提示字元執行以下動作。
    
    1.  從 Exchange 2013 安裝媒體執行以下命令，以停用 Active Directory 分割權限。
        
            setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
    
    2.  重新啟動組織中的 Exchange 2013 伺服器，或等候 Active Directory 存取 Token 複寫您的所有 Exchange 2013 伺服器。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您在組織中有Exchange 2010伺服器，您也需要重新啟動這些伺服器。</td>
        </tr>
        </tbody>
        </table>


2.  從 Exchange 管理命令介面執行下列動作：
    
    1.  建立Active Directory系統管理員角色群組。除了建立角色群組，命令會建立新的角色群組和建立郵件收件者角色與安全性群組建立和成員資格角色之間的一般角色指派。
        
            New-RoleGroup "Active Directory Administrators" -Roles "Mail Recipient Creation", "Security Group Creation and Membership"
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您想要能夠建立角色指派此角色群組的成員，包括角色管理角色。您不需要立即將此角色。不過，如果您想要將 [建立郵件收件者角色 」 或 「 安全性群組建立與成員資格的角色指派給其他角色 assignees，角色管理角色必須指派給此新的角色群組。遵循的步驟Active Directory系統管理員角色群組設定為可委派這些角色的唯一角色群組。</td>
        </tr>
        </tbody>
        </table>
    
    2.  使用以下命令在新角色群組和「建立郵件收件者」角色及「安全性群組建立及成員資格」角色之間建立委派角色指派。
        
            New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Active Directory Administrators" -Delegating
            New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Active Directory Administrators" -Delegating
    
    3.  使用下列命令將成員加入至新的角色群組。
        
            Add-RoleGroupMember "Active Directory Administrators" -Member <user to add>
    
    4.  取代新角色群組上的委派清單，如此就只有角色群組的成員可以新增或移除成員。
        
            Set-RoleGroup "Active Directory Administrators" -ManagedBy "Active Directory Administrators"
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>組織管理角色群組或使用者可以使用已指派角色管理角色的成員是直接或透過其他角色群組或 USG，可以略過此委派安全性檢查。若要防止任何Exchange管理員新增至新的角色群組的値，您必須移除角色指派的角色管理角色與任何Exchange管理員之間並將其指派給其他角色群組。</td>
        </tr>
        </tbody>
        </table>
    
    5.  尋找所有一般和委派角色指派給使用下列命令建立郵件收件者角色。此命令只會顯示**Name**、 **Role**，以及**RoleAssigneeName**屬性。
        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    6.  使用以下命令移除與新角色群組或任何其他角色群組不關聯之郵件收件者建立角色的所有規則和委派角色指派、USG 或是您要保留的直接指派。
        
            Remove-ManagementRoleAssignment <Mail Recipient Creation role assignment to remove>
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您想要移除的所有規則和委派角色指派給Active Directory系統管理員角色群組以外的任何角色受託人上建立郵件收件者角色，請使用下列命令。<em>WhatIf</em>參數可讓您查看將移除何種角色指派。移除<em>WhatIf</em>交換器並再次執行命令移除角色指派。</td>
        </tr>
        </tbody>
        </table>
        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
    
    7.  尋找所有一般和委派角色指派給安全性群組建立與成員資格角色使用下列命令。此命令只會顯示**Name**、 **Role**，以及**RoleAssigneeName**屬性。
        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    8.  使用以下命令移除與新角色群組或任何其他角色群組、USG 或是您要保留的直接指派無關聯之「安全性群組建立及成員資格」角色的所有一般和委派角色指派。
        
            Remove-ManagementRoleAssignment <Security Group Creation and Membership role assignment to remove>
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您可以使用前面附註中的同一命令，針對任何角色受託人 (非 Active Directory Administrators 角色群組) 移除「安全性群組建立及成員資格」角色的所有一般和委派角色指派，如以下範例所示。</td>
        </tr>
        </tbody>
        </table>
        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

如需詳細的語法及參數資訊，請參閱下列主題：

  - [New-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638181\(v=exchg.150\))

  - [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))

  - [Add-RoleGroupMember](https://technet.microsoft.com/zh-tw/library/dd638207\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/zh-tw/library/dd638182\(v=exchg.150\))

  - [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))

  - [Remove-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351205\(v=exchg.150\))

## 切換至 Active Directory 分割權限

您可以設定Exchange 2013組織的Active Directory分割權限。Active Directory分割權限完全移除權限可讓Exchange管理員及伺服器從Active Directory中建立安全性主體或修改這些物件的非Exchange屬性。當您已完成時，只有Active Directory系統管理員將能夠建立Active Directory安全性主體。這表示Exchange系統管理員將不能夠使用下列 cmdlet：

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

  - **Update-DistributionGroupMember**

Exchange系統管理員和伺服器將只能夠管理現有的Active Directory安全性主體的Exchange屬性。不過，他們將能夠建立及管理Exchange-特定物件，例如傳輸規則和整合通訊撥號對應表。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>啟用Active Directory之後分割權限、 Exchange管理員及伺服器將不再能夠在Active Directory、 中建立安全性主體與他們不能管理通訊群組成員資格。必須使用Active Directory管理工具具有必要的Active Directory權限執行這些工作。進行這項變更之前，您應該了解它對您的管理程序和整合Exchange 2013及的 RBAC 權限模型的協力廠商應用程式的影響。<br />
如需詳細資訊，請參閱<a href="understanding-split-permissions-exchange-2013-help.md">了解分割權限</a>中的＜Active Directory 分割權限＞一節。</td>
</tr>
</tbody>
</table>


若要從共用權限或 RBAC 分割權限切換至 Active Directory 分割權限，請執行以下動作：

1.  在 Windows 命令介面中，從 Exchange 2013 安裝媒體執行以下命令，以啟用 Active Directory 分割權限。
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:true

2.  如果您的組織中有多個 Active Directory 網域，您必須在每一個含有 Exchange 伺服器或物件的子網域執行 `setup.exe /PrepareDomain`，或從每一個網域所擁有的 Active Directory 伺服器的站台執行 `setup.exe /PrepareAllDomains`。

3.  重新啟動組織中的 Exchange 2013 伺服器，或等候 Active Directory 存取 Token 複寫您的所有 Exchange 2013 伺服器。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您在組織中有Exchange 2010伺服器，您也需要重新啟動這些伺服器。</td>
    </tr>
    </tbody>
    </table>

