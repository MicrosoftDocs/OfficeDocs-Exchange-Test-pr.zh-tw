---
title: '安裝 Exchange UM 疑難排解工具: Exchange 2013 Help'
TOCTitle: 安裝 Exchange UM 疑難排解工具
ms:assetid: 84223af0-a717-49ee-add6-86313bb30d17
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff844714(v=EXCHG.150)
ms:contentKeyID: 56271550
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安裝 Exchange UM 疑難排解工具

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange 2010 UM 疑難排解工具是名為 **Test-ExchangeUMCallFlow** 的 Exchange 管理命令介面指令程式。您可以使用指令程式來診斷自動答錄案例的特定組態錯誤，以及測試語音信箱在內部部署和跨單位部署 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更新版本的 UM 中是否正常運作。您可以在具有 Microsoft Office Microsoft Lync Server 2010 或更新版本的部署或具有 Vo IP 閘道、IP PBX 或工作階段邊界控制器 (SBC) 的 UM 部署中使用此指令程式。

UM 疑難排解工具可以安裝在本機 Unified Messaging Server、Exchange 2013 Mailbox Server 或其他 64 位元電腦上。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘

  - 安裝 UM 疑難排解工具之前，您必須在執行 Windows Vista、Windows 7、Windows 8 或 64 位元版本的 Windows Server 2008 或 Windows Server 2012 或更新版本的電腦上安裝下列元件：
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1) 請參閱[Microsoft.NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)。
    
      - 如果Windows Vista或Windows Server 2008電腦上執行此工具，請參閱[Windows Vista x64、 和 Windows Server 2008 x64 的 Microsoft.NET Framework 3.5 Family 更新](https://go.microsoft.com/fwlink/p/?linkid=178998)。
    
      - Windows 遠端管理 (WinRM) 2.0 和 Windows PowerShell V2 (Windows6.0-KB968930.msu)。請參閱 Microsoft 知識庫文章 968930：[Windows 管理架構核心套件 (Windows PowerShell 2.0 和 WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。
    
      - Microsoft Unified Communications Managed 的 API 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi)。請參閱[Unified 的 Communications Managed API 2.0 Core Runtime （64 位元）](https://go.microsoft.com/fwlink/p/?linkid=198175)。

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


## 安裝 UM 疑難排解工具

1.  從[Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?linkid=182625)，下載整合通訊疑難排解工具並連按兩下 MicrosoftExchange2010UMTroubleshootingTool.msi 安裝資料夾。

2.  在 **\[歡迎使用 Microsoft Exchange 2010 UM 疑難排解工具安裝嚮導\]** 頁面上，按 **\[下一步\]**。

3.  在 **\[使用者授權合約\]** 頁面上，檢閱軟體授權條款，如果您同意，請按一下 **\[我接受授權合約中的條款\]**，然後按 **\[下一步\]**。

4.  在 **\[選取安裝資料夾\]** 頁面上，確認安裝資料夾的路徑，然後按 **\[下一步\]**。

5.  在 **\[確認安裝\]** 頁面上，按 **\[下一步\]** 開始安裝。

6.  在 **\[安裝完成\]** 頁面上，按一下 **\[關閉\]**。

