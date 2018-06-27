---
title: '如需共用權限設定 Exchange 2013: Exchange 2013 Help'
TOCTitle: 如需共用權限設定 Exchange 2013
ms:assetid: 7d119977-b420-4b66-acf0-0a978b188cdd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638146(v=EXCHG.150)
ms:contentKeyID: 50473586
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 如需共用權限設定 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

共用權限可以讓您的 Microsoft Exchange Server 2013，系統管理員身分建立Active Directory安全性主體，如使用者並再將它們設定為Exchange收件者。不同分割權限、 分隔Exchange系統管理員群組和Active Directory管理員之間的管理工作，請於有不進行分隔的任務與共用權限。

如需共用與分割權限的相關資訊，請參閱[了解分割權限](understanding-split-permissions-exchange-2013-help.md)。

您可以設定Exchange 2013組織共用的權限如果您先前已將您的組織分割權限。切換至共用權限的程序會根據目前使用角色型存取控制 (RBAC) 分割權限是否不同或Active Directory分割權限。選擇的程序可適用於您目前的設定。以下是 true，如果您的組織使用Active Directory分割權限：

  - Microsoft Exchange保護群組組織單位 (OU) 存在。

  - Exchange Windows權限安全性群組位於 Microsoft Exchange保護群組 OU。

  - Exchange受信任子系統安全性群組是ExchangeWindows權限安全性群組的成員。

  - 有建立郵件收件者角色或安全性群組建立與成員資格的角色不正常的管理角色指派。

如果您永不設定您的組織分割權限，您不需要執行此程序。Exchange 2013會針對預設共用權限。

如需管理角色群組、管理角色以及一般與委派管理角色指派的相關資訊，請參閱下列主題：

  - [了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)

  - [了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)

  - [了解管理角色](understanding-management-roles-exchange-2013-help.md)

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

要尋找相關的權限的其他管理工作嗎？取出[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 您必須使用 Windows PowerShell、 Windows 命令介面中，或兩者，才能執行這些程序。如需詳細資訊，請參閱每項程序。

  - Exchange 2013組織必須目前設定的 RBAC 或Active Directory分割權限。

  - 如果您在組織中有 Microsoft Exchange Server 2010伺服器，您所選取的權限模型也會套用至這些伺服器。

  - 您必須要委派 「 建立郵件收件者管理 」 角色的安全性群組建立和組織管理管理角色群組或另一個已指派 「 郵件收件者 」 角色的角色群組的成員資格管理角色的權限。

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

## 切換從 RBAC 分割共用權限的權限

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色群組」項目。

若要切換從 RBAC 分割Exchange 2013共用權限的權限，您必須將 「 建立郵件收件者 」 角色與安全性群組建立與成員資格角色指派給也都會指定的收件者角色且已為成員的Exchange 2013系統管理員角色群組。在預設的共用權限設定， 組織管理角色群組包含每個角色。因此， 組織管理角色群組是在此程序。

## 設定共用的權限

若要設定共用的權限組織管理角色群組上，執行下列動作使用委派角色指派的 「 建立郵件收件者 」 角色與安全性群組建立與成員資格角色的權限的帳戶：

1.  新增建立郵件收件者角色與安全性群組建立與成員資格角色委派角色指派到組織管理角色群組使用下列命令。
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management" -Delegating
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management" -Delegating
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>具有委派角色指派的 「 建立郵件收件者角色及安全性群組建立與成員資格角色的角色群組 （在此程序， Active Directory系統管理員角色群組） 必須被指派角色管理角色可執行<strong>New-ManagementRoleAssignment</strong>指令程式。可委派角色管理角色的角色受託人必須將該角色指派給Active Directory系統管理員角色群組中。</td>
    </tr>
    </tbody>
    </table>


2.  新增 「 建立郵件收件者 」 角色的一般角色指派給使用下列命令組織管理和收件者管理角色群組。
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Recipient Management"

3.  新增安全性群組建立與成員資格角色的一般角色指派至組織管理角色群組使用下列命令。
    
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

## 從 Active Directory 管理員 （選用） 移除權限

您可以選擇性地移除授與給Active Directory管理員如果您不想再他們能夠建立或管理使用Exchange管理工具的Active Directory物件的權限。如果您想要移除Active Directory系統管理員的權限，請執行此程序。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然您可以移除Active Directory系統管理員可以管理使用Exchange管理工具的Active Directory物件的權限，可以繼續Active Directory系統管理員管理Active Directory物件及其Active Directory權限允許它會使用Active Directory管理工具]。不，但要能夠管理Exchange- Active Directory物件的特定屬性。如需詳細資訊，請參閱<a href="understanding-split-permissions-exchange-2013-help.md">了解分割權限</a>。</td>
</tr>
</tbody>
</table>


若要移除Exchange-相關的分割權限從Active Directory管理員執行下列動作：

1.  移除一般和委派角色指派的 「 建立郵件收件者 」 角色指派給角色群組或萬用安全性群組 (USG)，其中包含Active Directory管理員為使用下列命令的成員。此命令會使用Active Directory系統管理員角色群組做為範例。*WhatIf*參數可讓您查看將移除何種角色指派。移除*WhatIf*交換器並再次執行命令移除角色指派。
    
        Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

2.  移除一般和委派的安全性群組建立與成員資格的角色指派給角色群組或 USG 包含Active Directory管理員使用下列命令的成員身分的角色指派。此命令會使用Active Directory系統管理員角色群組做為範例。*WhatIf*參數可讓您查看將移除何種角色指派。移除*WhatIf*交換器並再次執行命令移除角色指派。
    
        Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

3.  選用的。如果您要從Active Directory系統管理員移除所有Exchange權限，您可以都移除的角色群組或 USG 它們成員。如需如何移除角色群組的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱[Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))或[Remove-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351205\(v=exchg.150\))。

## 從 Active Directory 分割共用權限的權限切換

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「Active Directory 分割權限」項目。

從Active Directory分割權限切換至Exchange 2013共用權限，您必須重新執行Exchange停用Active Directory分割權限在Exchange部署組織中的安裝程式並再建立角色群組和建立郵件收件者角色與安全性群組建立與成員資格角色之間的角色指派。在預設的共用權限設定， 組織管理角色群組包含每個角色。因此， 組織管理角色群組是在此程序。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此程序中的 setup.com 命令會針對Active Directory進行變更。您必須使用已可進行這些變更所需的權限的帳戶。此帳戶可能不是相同的帳戶已建立使用<strong>New-ManagementRoleAssignment</strong>指令程式的角色指派的權限。使用順利完成此程序中的每個步驟所需的權限的帳戶或帳戶。</td>
</tr>
</tbody>
</table>


若要從切換Active Directory分割共用權限的權限，請執行下列動作：

1.  從Windows命令介面中，執行下列命令在Exchange 2013安裝媒體中停用Active Directory分割權限。
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false

2.  從Exchange管理命令介面，執行下列命令以新增 「 建立郵件收件者 」 角色與安全性群組建立和管理角色和組織管理和收件者管理角色群組之間的一般角色指派。
    
        New-ManagementRoleAssignment "Mail Recipient Creation_Organization Management" -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Security Group Creation and Membership_Org Management" -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Mail Recipient Creation_Recipient Management" -Role "Mail Recipient Creation" -SecurityGroup "Recipient Management"

3.  重新啟動Exchange 2013伺服器在組織中。
    
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


如需詳細的語法及參數資訊，請參閱 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))。

