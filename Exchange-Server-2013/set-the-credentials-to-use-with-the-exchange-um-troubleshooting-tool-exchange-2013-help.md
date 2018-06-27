---
title: '設定 Exchange UM 疑難排解工具搭配使用的認證: Exchange 2013 Help'
TOCTitle: 設定 Exchange UM 疑難排解工具搭配使用的認證
ms:assetid: 542b7718-9345-40cc-bcb2-e307e70a1fa2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff630916(v=EXCHG.150)
ms:contentKeyID: 56271548
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Exchange UM 疑難排解工具搭配使用的認證

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange 2010 UM 疑難排解工具是名為 **Test-ExchangeUMCallFlow** 的 Exchange 管理命令介面指令程式。您可以使用指令程式來診斷自動答錄案例的特定組態錯誤，以及測試語音信箱在內部部署和跨單位部署 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更新版本的 UM 中是否正常運作。您可以在具有 Microsoft Office Microsoft Lync Server 2010 或更新版本的部署或具有 Vo IP 閘道、IP PBX 或工作階段邊界控制器 (SBC) 的 UM 部署中使用此指令程式。

依預設，在您執行 UM 疑難排解工具時，該工具會使用您登入電腦時所用的認證。所用的認證是為呼叫方指定的認證。您必須設定或指定在 `SIPClient` 模式下執行 UM 疑難排解工具時要使用的認證。但在 `Gateway` 模式下執行 UM 疑難排解工具時，則無需設定認證。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「 UM 伺服器 」 或者 「 UM 服務？[整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的項目。

  - 請確定您的Exchange 2010或 Exchange 2013 組織符合下列需求：
    
      - 已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。
    
      - 已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。
    
      - 已建立 UM IP 閘道。如需詳細步驟，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)。
    
      - 已新增 Exchange 2010 UM server 至 UM 撥號對應表。如果您使用 Exchange 2013 與 Lync Server，新增至 SIP URI 撥號對應所有用戶端存取和信箱伺服器。如需詳細步驟，請參閱[新增 UM 伺服器至撥號對應表](https://go.microsoft.com/fwlink/p/?linkid=313051)或[將信箱和用戶端存取伺服器新增至 SIP URI 撥號對應表](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)。

  - 安裝 UM 疑難排解工具。如需詳細步驟，請參閱[安裝 Exchange UM 疑難排解工具](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您將會使用 UM 疑難排解工具<code>SIPClient</code>模式中，有數個其他 Office Communications Server 2007 R2 或 Microsoft Lync Server 需求和先決條件。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=311961">檢查清單： 部署 Office Communications Server 2007 R2 和 Exchange 2010 Unified Messaging</a>或<a href="checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md">檢查清單： Lync Server 整合 Exchange 2013 UM</a>。</td>
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


## 設定與 UM 疑難排解工具搭配使用的認證

1.  從 **\[開始\]** 功能表中，開啟 **\[Microsoft Exchange 2010 UM 疑難排解工具\]**。

2.  在 **\[Microsoft Exchange 2010 UM 疑難排解工具\]** 視窗中，於提示字元處輸入以下命令，然後按 Enter。
    
        $cred=Get-Credential

3.  在 **\[Windows PowerShell 認證要求\]** 視窗中，輸入網域\\使用者名稱和密碼，然後按一下 **\[確定\]**。

4.  在 **\[Microsoft Exchange 2010 UM 疑難排解工具\]** 視窗中，指定必要的 Cmdlet 參數以測試呼叫流程。例如：
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

