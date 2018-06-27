---
title: '在 Windows 7 或 Windows 8 上執行 Exchange UM 疑難排解工具: Exchange 2013 Help'
TOCTitle: 在 Windows 7 或 Windows 8 上執行 Exchange UM 疑難排解工具
ms:assetid: 98d6869d-ee4a-4088-849d-ef75b0f5d932
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff851872(v=EXCHG.150)
ms:contentKeyID: 56271551
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Windows 7 或 Windows 8 上執行 Exchange UM 疑難排解工具

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange 2010 UM 疑難排解工具是名為 **Test-ExchangeUMCallFlow** 的 Exchange 管理命令介面指令程式。您可以使用指令程式來診斷自動答錄案例的特定組態錯誤，以及測試語音信箱在內部部署和跨單位部署 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更新版本的 UM 中是否正常運作。您可以在具有 Microsoft Office Microsoft Lync Server 2010 或更新版本的部署或具有 Vo IP 閘道、IP PBX 或工作階段邊界控制器 (SBC) 的 UM 部署中使用此指令程式。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「 UM 伺服器 」 或者 「 UM 服務？[整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的項目。

  - 請確定您的Exchange 2010或 Exchange 2013 組織符合下列需求：
    
      - 已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。
    
      - 已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。
    
      - 已建立 UM IP 閘道。如需詳細步驟，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)。
    
      - Exchange 2010 UM server 已新增至 UM 撥號對應表。如果您使用 Exchange 2013 和 Lync Server，新增至 SIP URI 撥號對應所有用戶端存取和信箱伺服器。如需詳細步驟，請參閱[新增 UM 伺服器至撥號對應表](https://go.microsoft.com/fwlink/p/?linkid=313051)或[將信箱和用戶端存取伺服器新增至 SIP URI 撥號對應表](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)。

  - 如果您正在Exchange 2010 SP1 本機 UM 伺服器上執行 UM 疑難排解工具或更新版本或 Exchange 2013 Mailbox server 上，您可能沒有安裝下面所列的所有必要軟體。他們可能已安裝與 UM 伺服器角色。不過，如果您不執行 UM 伺服器角色的伺服器 64 位元電腦上安裝 UM 疑難排解工具，您將需要安裝下列元件：
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)。請參閱[Microsoft.NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)。
    
      - 如果Windows Vista 或Windows Server 2008電腦上執行此工具，請參閱[Windows Vista x64，及 Windows Server 2008 x64 的 Microsoft.NET Framework 3.5 Family 更新](https://go.microsoft.com/fwlink/p/?linkid=178998)。
    
      - Windows 遠端管理 (WinRM) 2.0 和 Windows PowerShell V2 (Windows6.0-KB968930.msu)。請參閱 Microsoft 知識庫文章 968930：[Windows 管理架構核心套件 (Windows PowerShell 2.0 和 WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。
    
      - Microsoft Unified Communications Managed 的 API 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi)。請參閱[Unified 的 Communications Managed API 2.0 Core Runtime （64 位元）](https://go.microsoft.com/fwlink/p/?linkid=198175)。

  - 下載並安裝 UM 疑難排解工具。
    
      - 從 Microsoft 下載中心下載[整合通訊疑難排解工具](https://go.microsoft.com/fwlink/p/?linkid=182625) 。
    
      - 安裝此工具。如需詳細資訊，請參閱[安裝 Exchange UM 疑難排解工具](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您將會使用 UM 疑難排解工具<code>SIPClient</code>模式中，有數個其他 Office Communications Server 2007 R2 或Microsoft Lync Server 需求和必須符合的先決條件。如需詳細資訊，<a href="https://go.microsoft.com/fwlink/p/?linkid=311961">檢查清單： 部署 Office Communications Server 2007 R2 和 Exchange 2010 Unified Messaging</a>。</td>
        </tr>
        </tbody>
        </table>


  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 在 Windows Vista、Windows 7 或 Windows 8 上執行 UM 疑難排解工具

1.  依序按一下 **\[開始\]** \> **\[所有程式\]** \> **\[附屬應用程式\]** \> **\[Windows PowerShell\]**。

2.  在 **\[Windows PowerShell\]** 上按一下滑鼠右鍵，然後從快顯功能表中選取 **\[以系統管理員身分執行\]**。

3.  在 Windows PowerShell 命令提示字元下，移至安裝 UM 疑難排解工具的資料夾，並執行下列命令。
    
        C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -psconsolefile .\Microsoft.Exchange.UM.TroubleshootingToolsnapin.psc1 -noexit -command ". '.\Microsoft.Exchange.UM.TroubleshootingTool.ps1' "

4.  如果您要在 Windows Vista、Windows 7 或 Windows 8 上執行 UM 疑難排解工具，則請在 Windows PowerShell 命令提示字元下執行下列命令。
    
        Set-ExecutionPolicy RemoteSigned

5.  從 **\[開始\]** 功能表中，開啟 **\[Microsoft Exchange 2010 UM 疑難排解工具\]**。

6.  在 **\[Microsoft Exchange 2010 UM 疑難排解工具\]** 視窗中，於提示字元處輸入以下命令，然後按 Enter。
    
        $cred=Get-Credential

7.  在 **\[Windows PowerShell 認證要求\]** 視窗中，輸入網域\\使用者名稱和密碼，然後按一下 **\[確定\]**。

8.  在 **\[Microsoft Exchange 2010 UM 疑難排解工具\]** 視窗中，指定測試呼叫流程所需的 Cmdlet 參數。例如：
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

