---
title: 'Exchange 2013 必要條件: Exchange 2013 Help'
TOCTitle: Exchange 2013 必要條件
ms:assetid: e21cf744-7813-48b3-9293-5cecd89a6c25
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb691354(v=EXCHG.150)
ms:contentKeyID: 50474420
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 必要條件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-03-20_

本主題針對 Microsoft Exchange 2013 Mailbox、Client Access 和 Edge Transport server role，提供安裝必要的 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 Service Pack 1 (SP1) 作業系統先決條件的步驟。另外也提供在 Windows 8、Windows 8 1 和 Windows 7 用戶端電腦上安裝 Exchange 2013 管理工具所需的先決條件。

  - 開始之前有哪些須知？

  - Active Directory 準備

  - Windows Server 2012 R2 和 Windows Server 2012 先決條件
    
      - Mailbox 或 Client Access server role
    
      - Edge Transport server role

  - Windows Server 2008 R2 SP1 先決條件
    
      - Mailbox 或 Client Access server role
    
      - Edge Transport server role

  - Windows 7 必要條件 (僅系統管理工具)

  - Windows 8 和 Windows 8.1 必要條件 (僅系統管理工具)

## 開始之前有哪些須知？

  - 本主題中的資訊適用於 Service Pack 1 和更新版本的 Exchange 2013。

  - Edge Transport server role 從 Exchange 2013 SP1 開始提供使用。

  - 請確定您的樹系的功能層級至少是 Windows Server 2003，而且架構主機執行的是 Windows Server 2003 Service Pack 2 或更新版本。如需有關 Windows 功能層級的詳細資訊，請參閱[管理網域及樹系](https://go.microsoft.com/fwlink/p/?linkid=137037)。

  - 對於執行 Exchange 2013 server role 或管理工具的所有伺服器，必須使用 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 SP1 的完整安裝選項。

  - 您必須首先將您的電腦加入相應的內部 Active Directory 樹系和網域。

  - 一些先決條件要求您重新開機伺服器以完成安裝。

  - 在您的電腦上安裝最新的 Windows 更新。如需詳細資訊，請參閱 [部署安全性檢查清單](deployment-security-checklist-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果是安裝 Mailbox server role，且想要將此伺服器作為資料庫可用性群組 (DAG) 的成員，則必須執行 Windows Server 2012 R2 Standard 或 Datacenter Edition、Windows Server 2012 Standard 或 Datacenter Edition，或是 Windows Server 2008 R2 SP1 Enterprise Edition。Windows Server 2008 R2 SP 1 Standard Edition 不支援 DAG 所需的功能。<br />
    如果伺服器上已安裝 Exchange，則無法升級 Windows。<br />
    若要升級 Microsoft Unified Communications Managed API (UCMA) 4.0，您必須首先解除安裝所有使用 [新增/移除] 程式安裝的 UCMA 早期版本。</td>
    </tr>
    </tbody>
    </table>


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


## Active Directory 準備

您要用於為 Exchange 2013 準備 Active Directory 的電腦必須滿足一些特定先決條件。

在用於準備 Active Directory 的電腦上，依所示順序安裝下列軟體：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (隨付於 Windows Server 2012 R2)

在您安裝完上述軟體後，請完成下列步驟，安裝 Remote Tools Administration Pack。安裝 Remote Tools Administration Pack 之後，您就可以使用此電腦來準備 Active Directory。如需有關準備 Active Directory 的詳細資訊，請參閱＜[準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md)＞。

1.  開啟 \[Windows PowerShell\]。

2.  安裝 Remote Tools Administration Pack。
    
      - 在 Windows Server 2012 R2 或 Windows Server 2012 電腦上，執行下列命令。
        
            Install-WindowsFeature RSAT-ADDS
    
      - 在 Windows Server 2008 R2 SP1 電腦上，執行下列命令。
        
            Add-WindowsFeature RSAT-ADDS

## Windows Server 2012 R2 和 Windows Server 2012 先決條件

在 Windows Server 2012 R2 或 Windows Server 2012 電腦上安裝 Exchange 2013 所需的先決條件，視您想要安裝的 Exchange 角色而定。閱讀以下與您要安裝的角色相符之區段。

## Mailbox 或 Client Access server role

在您想要執行下列其中一個動作的 Windows Server 2012 R2 或 Windows Server 2012 電腦上，依照本節的指示來安裝先決條件：

  - 僅於電腦上安裝 Mailbox server role。

  - 僅於電腦上安裝 Client Access server role。

  - 在同一台電腦安裝信箱與用戶端存取伺服器角色。

執行下列操作來安裝所需的 Windows 角色和功能：

1.  開啟 \[Windows PowerShell\]。

2.  執行下列命令來安裝所需的 Windows 元件。
    
        Install-WindowsFeature AS-HTTP-Activation, Desktop-Experience, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS

安裝作業系統角色與功能後，請依照以下顯示順序安裝軟體：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 2013 CU16 和更新版本<strong>需要</strong> .NET Framework 4.6.2。安裝 Exchange 2013 CU16 之前請將伺服器升級至 .NET Framework 4.6.2，否則會收到錯誤訊息。如果您的 Exchange 伺服器上安裝了 .NET Framework 4.5.2，在安裝 .NET Framework 4.6.2 之前請將伺服器升級至 Exchange 2013 CU15。</td>
    </tr>
    </tbody>
    </table>


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (隨付於 Windows Server 2012 R2)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Edge Transport server role

在您想要在電腦上安裝 Edge Transport server role 的 Windows Server 2012 R2 或 Windows Server 2012 上，依照本節的指示來安裝先決條件：

執行下列操作來安裝所需的 Windows 角色和功能：

1.  開啟 \[Windows PowerShell\]。

2.  執行下列命令來安裝所需的 Windows 元件。
    
        Install-WindowsFeature ADLDS

安裝對應於您要安裝之 Exchange 2013 版本的 Windows Management Framework 版本。

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 2013 CU16 和更新版本<strong>需要</strong> .NET Framework 4.6.2。安裝 Exchange 2013 CU16 之前請將伺服器升級至 .NET Framework 4.6.2，否則會收到錯誤訊息。如果您的 Exchange 伺服器上安裝了 .NET Framework 4.5.2，在安裝 .NET Framework 4.6.2 之前請將伺服器升級至 Exchange 2013 CU15。</td>
    </tr>
    </tbody>
    </table>


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (隨付於 Windows Server 2012 R2)

## Windows Server 2008 R2 SP1 先決條件

在 Windows Server 2008 R2 SP1 電腦上安裝 Exchange 2013 所需的先決條件，視您想要安裝的 Exchange 角色而定。閱讀以下與您要安裝的角色相符之區段。

## Mailbox 或 Client Access server role

請按照本節中的說明在 Windows Server 2008 R2 SP1 電腦 (您想要執行下列一個動作) 上安裝先決條件：

  - 僅於電腦上安裝 Mailbox server role。

  - 僅於電腦上安裝 Client Access server role。

  - 在同一台電腦安裝信箱與用戶端存取伺服器角色。

執行下列操作來安裝所需的 Windows 角色和功能：

1.  開啟 \[Windows PowerShell\]。

2.  執行下列命令以載入伺服器管理員模組。
    
        Import-Module ServerManager

3.  執行下列命令來安裝所需的 Windows 元件。
    
        Add-WindowsFeature Desktop-Experience, NET-Framework, NET-HTTP-Activation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Web-Server, WAS-Process-Model, Web-Asp-Net, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, RSAT-ADDS

安裝作業系統角色與功能後，請依照以下顯示順序安裝軟體：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 2013 CU16 和更新版本<strong>需要</strong> .NET Framework 4.6.2。安裝 Exchange 2013 CU16 之前請將伺服器升級至 .NET Framework 4.6.2，否則會收到錯誤訊息。如果您的 Exchange 伺服器上安裝了 .NET Framework 4.5.2，在安裝 .NET Framework 4.6.2 之前請將伺服器升級至 Exchange 2013 CU15。</td>
    </tr>
    </tbody>
    </table>


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://go.microsoft.com/fwlink/p/?linkid=258269)

4.  [Microsoft 知識庫文章 KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=974405)

5.  [知識庫文章 KB2619234（啟用用於 RPC over HTTP 的 Association Cookie/GUID 以於 Windows 7 及 Windows Server 2008 R2 中的 RPC 層使用)](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2619234)

6.  [知識庫文章 KB2533623（不安全的 程式庫載入可能允許程式碼執行）](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2533623)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您已在電腦上將 Windows Update 設定安裝安全更新，則此 hotfix 可能已安裝。</td>
    </tr>
    </tbody>
    </table>


## Edge Transport server role

請按照本節中的說明在 Windows Server 2008 R2 SP1 電腦 (您想要安裝 Edge Transport server role 的電腦) 上安裝先決條件：

執行下列操作來安裝所需的 Windows 角色和功能：

1.  開啟 \[Windows PowerShell\]。

2.  執行下列命令以載入伺服器管理員模組。
    
        Import-Module ServerManager

3.  執行下列命令來安裝所需的 Windows 元件。
    
        Add-WindowsFeature NET-Framework, ADLDS

安裝作業系統角色與功能後，請依照以下顯示順序安裝軟體：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 2013 CU16 和更新版本<strong>需要</strong> .NET Framework 4.6.2。安裝 Exchange 2013 CU16 之前請將伺服器升級至 .NET Framework 4.6.2，否則會收到錯誤訊息。如果您的 Exchange 伺服器上安裝了 .NET Framework 4.5.2，在安裝 .NET Framework 4.6.2 之前請將伺服器升級至 Exchange 2013 CU15。</td>
    </tr>
    </tbody>
    </table>


2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Windows 7 必要條件 (僅系統管理工具)

在您想要安裝 Exchange 管理工具的已加入網域的 Windows 7 64 位元電腦，依照本節的指示來安裝先決條件：

1.  開啟 \[控制台\]，然後選取 \[程式集\]。

2.  按一下 **\[開啟或關閉 Windows 功能\]**。

3.  瀏覽至 **\[網際網路資訊服務\]** \> **\[Web 管理工具\]** \> **\[IIS 6 管理相容性\]**。

4.  選取 **\[IIS 6 管理主控台\]** 的核取方塊，再按一下 **\[確定\]**。

安裝作業系統功能後，請依照顯示順序安裝下列軟體：

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [知識庫文章 KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=974405)

## Windows 8 和 Windows 8.1 必要條件 (僅系統管理工具)

[.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

