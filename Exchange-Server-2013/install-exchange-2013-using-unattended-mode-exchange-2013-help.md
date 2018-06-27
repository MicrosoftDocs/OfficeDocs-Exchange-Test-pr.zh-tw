---
title: '使用自動模式安裝 Exchange 2013: Exchange 2013 Help'
TOCTitle: 使用自動模式安裝 Exchange 2013
ms:assetid: 386465e9-41da-4e26-9816-b3b69be1f8bf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997281(v=EXCHG.150)
ms:contentKeyID: 50472866
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用自動模式安裝 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-06-19_

若要執行自動安裝，則必須從命令提示字元安裝 Microsoft Exchange Server 2013。如需規劃與部署 Exchange 2013 的相關資訊，請參閱[規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

建議將 Edge Transport role 安裝在組織內部 Active Directory 樹系外的周邊網路中。雖然可以將 Edge Transport server role 安裝在加入網域的電腦上，但這樣只會啟用 Windows 功能和設定的網域管理。Edge Transport role 本身不使用 Active Directory。反之，它使用 Active Directory 輕量型目錄服務 (AD LDS) Windows 功能和儲存組態和收件者資訊。如需 Edge Transport role 的詳細資訊，請參閱＜[Edge Transport Server](edge-transport-servers-exchange-2013-help.md)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您是否曾聽過 Exchange Server 部署助理？這是一項免費的線上工具，該工具會詢問您一些問題並特別為您建立一份自訂的部署檢查清單，以協助您在組織中快速部署 Exchange 2013。若想要深入了解，請移至 <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 部署助理</a>。</td>
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
<td>在執行 Exchange 2013 的電腦上安裝任何伺服器角色之後，就無法使用 Exchange 2013 安裝精靈，將任何的其他伺服器角色新增至此電腦。如果想要將多個伺服器角色新增至電腦，則必須使用 [控制台] 的 [新增或移除程式]，或從 [命令提示字元] 視窗使用 Setup.exe。<br />
Edge Transport role 不能與 Mailbox 或 Client Access server role 安裝在相同的電腦上。</td>
</tr>
</tbody>
</table>


如需要在安裝後完成之工作的相關資訊，請參閱 [Exchange 2013 後續安裝工作](exchange-2013-post-installation-tasks-exchange-2013-help.md)。

## 開始之前有哪些須知？

下列資訊適用於所有 Exchange 2013 伺服器角色。

  - 在安裝 Exchange 2013前，請確認已閱讀版本資訊。如需詳細資訊，請參閱 [Exchange 2013 版本資訊](release-notes-for-exchange-2013-exchange-2013-help.md)。

  - 您安裝 Exchange 2013 的電腦必須有支援的作業系統 (例如 Windows Server 2008 R2 Service Pack 1 (SP1)、Windows Server 2012 R2 或 Windows Server 2012)、有足夠的磁碟空間，且符合其他需求。如需系統需求的相關資訊，請參閱 [Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 若要執行 Exchange 2013 安裝程式，您必須安裝 Microsoft .NET Framework 4.5、Windows Management Framework 及其他必要軟體。若要了解所有伺服器角色的必要條件，請參閱 [Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在伺服器上安裝 Exchange 之後，就不得變更伺服器名稱。在安裝 Exchange 伺服器角色之後，就不支援重新命名伺服器。</td>
</tr>
</tbody>
</table>


下列資訊適用於 Exchange 2013 Mailbox 和 Client Access server role。

  - 預估完成時間：60 分鐘

  - 每個組織的 Active Directory 樹系中至少都要有一部 Client Access Server 與一部 Mailbox Server。此外，每個含有 Mailbox Server 的 Active Directory 網站也至少要包含一部 Client Access Server。如果您要分離您的伺服器角色，建議您先安裝 Mailbox server role。

  - 您安裝 Exchange 2013 的電腦必須是 Active Directory 網域的成員。

  - 如果您尚未準備 Active Directory 架構，則必須確定使用的帳戶委派了 Schema Admins 群組的成員資格。如果是安裝組織中的第一部 Exchange 2013 伺服器，您使用的帳戶必須具有 Enterprise Admins 群組的成員資格。如果已準備好架構，並且不是安裝組織中的第一部 Exchange 2013 伺服器，則您使用的帳戶必須屬於 Exchange 2013 組織管理角色群組的成員。
    
    身為「委派安裝」角色群組成員的系統管理員，可部署先前已由「組織管理」角色群組的成員提供的 Exchange 2013 伺服器。

下列資訊適用於 Exchange 2013 Edge Transport server role。

  - 預估完成時間：40 分鐘

  - Exchange 2013 SP1 或更新版本提供 Edge Transport role。

  - 您必須在電腦上設定主要 DNS 尾碼。例如，如果電腦的完整網域名稱是 edge.contoso.com，則電腦的 DNS 尾碼是 contoso.com。如需詳細資訊，請參閱＜[主要 DNS 尾碼遺漏](primary-dns-suffix-is-missing-exchange-2013-help.md)＞。

  - Exchange 2007 和 Exchange 2010 Hub Transport Server 需要更新，您才能在它們與 Exchange 2013 Edge Transport Server 之間建立 EdgeSync 訂閱。如果您未安裝此更新，EdgeSync 訂閱將無法正常運作。如需詳細資訊，請參閱＜[Exchange 2013 系統需求](exchange-2013-system-requirements-exchange-2013-help.md)＞的＜支援的共存案例＞一節。

  - 請確定您使用的帳戶是您安裝 Edge Transport role 的電腦上的本機 Administrators 群組的成員。

## 在自動模式中使用 Setup.exe 安裝 Exchange 2013

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要下載最新版本的 Exchange 2013，請參閱＜<a href="updates-for-exchange-2013-exchange-2013-help.md">更新 Exchange 2013</a>＞。</td>
</tr>
</tbody>
</table>


1.  登入要在其上安裝 Exchange 2013 的電腦。

2.  瀏覽至Exchange 2013安裝檔案的網路位置。

3.  在命令提示中，執行適合您組織的命令。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您已啟用使用者存取控制 (UAC)，必須從更高的命令提示字元安裝 <code>Setup.exe</code>。</td>
    </tr>
    </tbody>
    </table>
    
        Setup.exe [/Mode:<setup mode>] [/IAcceptExchangeServerLicenseTerms]
        [/Roles:<server roles to install>] [/InstallWindowsComponents] 
        [/OrganizationName:<name for the new Exchange organization>] 
        [/TargetDir:<target directory>] [/SourceDir:<source directory>]
        [/UpdatesDir:<directory from which to install updates>] 
        [/DomainController:<FQDN of domain controller>] [/DisableAMFiltering]
        [/AnswerFile:<filename>] [/DoNotStartTransport] 
        [/EnableErrorReporting] [/CustomerFeedbackEnabled:<True | False>] 
        [/AddUmLanguagePack:<UM language pack name>] 
        [/RemoveUmLanguagePack:<UM language pack name>] 
        [/NewProvisionedServer:<server>] [/RemoveProvisionedServer:<server>] 
        [/MdbName:<mailbox database name>] [/DbFilePath:<Edb file path>] 
        [/LogFolderPath:<log folder path>] [/ActiveDirectorySplitPermissions:<True | False>]
        [/TenantOrganizationConfig:<path>]

4.  安裝程式會在本機將安裝檔案複製到要安裝 Exchange 2013 的電腦上。

5.  安裝程式會檢查必要條件 (含所安裝之伺服器角色特有的所有必要條件)。如果尚未符合所有必要條件，則安裝程式會失敗，並會傳回說明失敗原因的錯誤訊息。如果已符合所有必要條件，則安裝程式會安裝 Exchange 2013。

6.  Exchange 2013 完成後請重新啟動電腦。

7.  執行 [Exchange 2013 後續安裝工作](exchange-2013-post-installation-tasks-exchange-2013-help.md) 中提供的工作以完成部署。

## 範例

以下是使用 Setup.exe 的範例：

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /OrganizationName:MyOrg /IAcceptExchangeServerLicenseTerms**
    
    這個命令會在 MyOrg Exchange 2013 中建立Active Directory 組織，安裝用戶端存取伺服器角色、信箱伺服器角色以及管理工具，並接受 Exchange 2013 授權條款。

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /TargetDir:"C:\\Exchange Server" /IAcceptExchangeServerLicenseTerms**
    
    這個命令會將用戶端存取伺服器角色、信箱伺服器角色及管理工具安裝至 "C:\\Exchange Server" 目錄。這個命令會假設Exchange 2013組織已就緒。

  - **Setup.exe /mode:Install /r:CA,MB /IAcceptExchangeServerLicenseTerms**
    
    這個命令會將用戶端存取伺服器角色、信箱伺服器角色及管理工具安裝至預設安裝位置。

  - **Setup.exe /mode:Install /r:EdgeTransport /IAcceptExchangeServerLicenseTerms**
    
    這個命令會將 Edge Transport server role 和管理工具安裝至預設安裝位置。

  - **Setup.exe /mode:Install /r:ET /IAcceptExchangeServerLicenseTerms**
    
    這個命令會將 Edge Transport server role 和管理工具安裝至預設安裝位置。

  - **Setup.exe /mode:Uninstall /IAcceptExchangeServerLicenseTerms**
    
    這個命令會從伺服器完全移除 Exchange 2013，以及從 Active Directory 移除這個伺服器的 Exchange 組態。

  - **Setup.exe /PrepareAD /on:"My Org" /IAcceptExchangeServerLicenseTerms**
    
    這個命令會建立一個名為 My Org 的 Exchange 組織，並為 Active Directory 準備 Exchange 2013。

  - **C:\\ExchangeServer\\bin\\Setup.exe /m:Install /r:ClientAccess /SourceDir:d:\\amd64 /IAcceptExchangeServerLicenseTerms**
    
    這個命令會使用 D:\\amd64 作為來源目錄，新增 Client Access Server role 至現有的 Exchange 2013 伺服器。

  - **Setup.exe /role:ClientAccess,Mailbox /UpdatesDir:"C:\\ExchangeServer\\New Patches" /IAcceptExchangeServerLicenseTerms**
    
    這個命令會使用指定目錄中的修補檔案更新 ExchangeServer.msi，然後安裝用戶端伺服器角色、信箱伺服器角色及管理工具。若此目錄包含語言套件組合，則代表已安裝語言套件。

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /DomainController:DC01 /IAcceptExchangeServerLicenseTerms**
    
    這個命令會在安裝用戶端存取伺服器角色、信箱伺服器角色及管理工具時，使用網域控制站 DC01 查詢及變更 Active Directory。

  - **Setup.exe /mode:Install /role:ClientAccess /AnswerFile:c:\\ExchangeConfig.txt /IAcceptExchangeServerLicenseTerms**
    
    這個命令會使用 ExchangeConfig.txt 檔案中的設定安裝用戶端存取角色。

  - **Setup.exe /rprs:Exchange03 /IAcceptExchangeServerLicenseTerms**
    
    這個命令會從 Active Directory 移除物件 Exchange03。

  - **Setup.exe /AddUmLanguagePack:ko-KR /IAcceptExchangeServerLicenseTerms**
    
    這個命令會從 %ExchangeSourceDir%\\ServerRoles\\UnifiedMessaging 目錄安裝韓文整合通訊語言套件。

## 如何知道這是否正常運作？

若要確認您是否已成功安裝 Exchange 2013，請參閱 [確認 Exchange 2013 安裝](verify-an-exchange-2013-installation-exchange-2013-help.md).

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

