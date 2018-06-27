---
title: '測試及疑難排解與 UM 疑難排解工具: Exchange 2013 Help'
TOCTitle: 測試及疑難排解與 UM 疑難排解工具
ms:assetid: 1fab2e52-bd2d-4e46-b222-53fee9d34cba
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg621148(v=EXCHG.150)
ms:contentKeyID: 56271544
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 測試及疑難排解與 UM 疑難排解工具

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange 2010 UM 疑難排解工具是名為 **Test-ExchangeUMCallFlow** 的 Exchange 管理命令介面指令程式。您可以使用指令程式來診斷自動答錄案例的特定組態錯誤，以及測試語音信箱在內部部署和跨單位部署 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更新版本的 UM 中是否正常運作。您可以在具有 Microsoft Office Microsoft Lync Server 2010 或更新版本的部署或具有 Vo IP 閘道、IP PBX 或工作階段邊界控制器 (SBC) 的 UM 部署中使用此指令程式。

## 概觀

此指令程式像通話，並執行一系列的協助識別設定錯誤的電話語音設備、 Exchange 2010 SP1 或更新版本整合通訊設定及內部部署與跨部門部署Exchange 2010 SP1 或更新版本整合通訊之間的連線問題的內部部署系統管理員的診斷測試。

執行此 Cmdlet 時，它會針對已偵測到的問題說明原因及可能的解決方案。它也會輸出一般音訊品質計量，可用來診斷與網路連線相關的音訊品質問題，如抖動和平均封包遺失。**Test-ExchangeUMCallFlow** Cmdlet 支援測試 `Secured`、`SIP Secured` 和 `Unsecured` 呼叫中的 UM 元件，可以在 `Gateway` 或 `SIPClient` 模式中執行。

根據預設，當您正在執行 UM 疑難排解工具，它會使用登入電腦時使用的認證。使用的認證是所指定的撥號方。您必須設定或指定`SIPClient`模式中執行 UM 疑難排解工具時要使用的認證。不過，您不需要`Gateway`模式中執行 UM 疑難排解工具時設定的認證。如果您將`SIPClient`模式中使用 UM 疑難排解工具，必須符合數個其他 Office Communications Server 2007 R2 或 Lync Server 需求和先決條件。如需詳細資訊，請參閱 ＜[檢查清單： 部署 Office Communications Server 2007 R2 和 Exchange 2010 Unified Messaging](https://go.microsoft.com/fwlink/p/?linkid=311961)或[檢查清單： Lync Server 整合 Exchange 2013 UM](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必須使用<strong>Test-ExchangeUMCallFlow</strong>指令程式來測試僅之語音信箱功能的 Microsoft Exchange Server 2010整合通訊伺服器Exchange 2010安裝 Service Pack 1 (SP1) 或 Microsoft Exchange 2013。</td>
</tr>
</tbody>
</table>


**Test-ExchangeUMCallFlow** Cmdlet 可以安裝在本機 Exchange 2010 Unified Messaging Server、Exchange 2013 Mailbox Server，或執行下列項目的其他 64 位元電腦上：

  - Windows 7 或 Windows 8 作業系統

  - Windows Server 2008 或 Windows Server 2008 R2 作業系統

  - Windows Server 2012 或 Windows Server 2012 R2 作業系統

安裝 **Test-ExchangeUMCallFlow** Cmdlet 之前，您必須已在 Windows 7、Windows 8、Windows Server 2008 或 Windows Server 2012 64 位元電腦上安裝下列元件：

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1)。若要下載的 service pack，請參閱[Microsoft.NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)。

  - Microsoft .NET Framework 3.5 Family 更新Windows Vista x64 和Windows Server 2008 x64 更新如果Windows Vista或Windows Server 2008電腦上執行此工具。若要下載更新，請參閱[Windows Vista x64、 和 Windows Server 2008 x64 的 Microsoft.NET Framework 3.5 Family 更新](https://go.microsoft.com/fwlink/p/?linkid=178998)。

  - Windows 遠端管理 (WinRM) 2.0 和 Windows PowerShell V2 (Windows6.0-KB968930.msu)。如需詳細資訊，請參閱 Microsoft 知識庫文章 968930：[Windows 管理架構核心套件 (Windows PowerShell 2.0 和 WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。

  - Unified 的 Communications Managed AP1 2.0，Core Runtime （64 位元）。若要下載 UcmaRuntimeWebDownloadX64.msi 程式檔，請參閱[Unified Communications Managed API 2.0，Core Runtime （64 位元）](https://go.microsoft.com/fwlink/p/?linkid=198175)。

**Test-ExchangeUMCallFlow** cmdlet 不包含在Exchange 2010 SP1 DVD、 Exchange 2010 SP1 唯讀下載或 Exchange 2013 安裝媒體;不過，您可以從[Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?linkid=182625)下載指令程式。

如需語法及參數的相關資訊，請參閱 [Test-ExchangeUMCallFlow](https://technet.microsoft.com/zh-tw/library/ff630913\(v=exchg.150\))。

