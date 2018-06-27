---
title: '了解 Exchange UM 疑難排解工具: Exchange 2013 Help'
TOCTitle: 了解 Exchange UM 疑難排解工具
ms:assetid: cc11bf5e-2c87-4495-b2ad-3e9a6bc81dbc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg584301(v=EXCHG.150)
ms:contentKeyID: 56271553
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解 Exchange UM 疑難排解工具

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange 2010整合通訊疑難排解工具是名為**Test-ExchangeUMCallFlow**Exchange管理命令介面 cmdlet。您可以使用這項工具在組織中進行一系列的診斷測試的整合通訊 (UM)。如果測試的任何失敗，此工具會報告失敗和可能的解決方案來修正此問題的原因。您只可以在Exchange 2010或更新版本的伺服器上使用 UM 疑難排解工具。

UM 疑難排解工具可測試在內部及跨部門部署時，語音信箱是否正確運作。您可以在包含 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 2010 或更新版本的 UM 部署中，或在包含 VoIP 閘道、IP 專用交換機 (IP PBX) 或工作階段邊界控制器 (SBC) 的 UM 部署中使用此工具。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UM 疑難排解工具是用於測試及疑難排解。反之，<strong>Test-UMConnectivity</strong> 指令程式則是用於監視。<strong>Test-UMConnectivity</strong> Cmdlet 可與用來監控 Exchange 2010 UM 伺服器或 Exchange 2013 Client Access Server 和 Mailbox Server 及電話語音元件的 System Center Operations Manager (SCOM) 管理組件搭配使用。<strong>Test-UMConnectivity</strong> 指令程式會執行本機 SCOM 測試及信箱的本機登入測試，也可當做 SCOM 工作來執行。</td>
</tr>
</tbody>
</table>


若要下載 UM 疑難排解工具，請參閱 ＜[整合通訊疑難排解工具](https://go.microsoft.com/fwlink/p/?linkid=182625)。

**目錄**

概觀

UM troubleshooting architecture

VoIP gateway and IP PBX deployments

Office Communications Server R2 and Microsoft Lync Server deployments

Installing the UM Troubleshooting Tool

Cmdlet parameters

## 概觀

UM 疑難排解工具可簡化 UM 部署的測試及疑難排解。執行 UM 疑難排解工具時，會自動產生一組儲存於 C:\\Users\\%UserProfile%\\AppData\\Roaming\\Microsoft Exchange 2010 UM Troubleshooting 資料夾的追蹤檔案。此工具會產生下列追蹤檔案：

  - **UMTool\_Collaboration** 包含 RTC 堆疊追蹤。

  - **UMTool\_DiagnosticLog** 列出所有執行的測試及其結果。

  - **UMTool\_S4** 包含 S4：信號堆疊追蹤。

  - **UMTool\_SIPMessageLogs** 包含對所撥測試呼叫的完整 SIP 追蹤。

UM 疑難排解工具可直接連線至內部部署工作階段邊界控制器 (SBC) (如果有)，或連線至資料中心的 SBC，並透過 VoIP 閘道或 IP PBX 模擬 PBX 的來電。UM 疑難排解工具可用於診斷：

  - 在部署 Office Communications Server 2007 R2 或 Microsoft Lync Server 之內部或跨部門 UM 部署中的錯誤設定。

  - 在包含 VoIP 閘道及 PBX 或 IP PBX 之內部或跨部門電話語音設備中的錯誤設定。

  - 網域名稱系統 (DNS) 的問題。

  - 使用 SIP 安全或安全 UM 撥號對應表時的憑證問題。

  - DTMF (也稱為按鍵式) 及音效的訊號及媒體問題。

如果 UM 疑難排解工具偵測到設定中的失敗，則工具會回報錯誤的原因及可能的因應解決方案。UM 疑難排解工具用於內部部署工具時，可回報的錯誤如下：

  - 已達到呼叫上限。

  - 並未啟用整合通訊的使用者。

  - 找不到 UM IP 閘道、撥號對應表或群組搜尋資訊。

  - 安全性類型不符合 UM 撥號對應表。

  - 沒有可處理呼叫的工作者處理序。

  - 已停止 UM 服務或 UM 呼叫路由器服務。

  - 找不到 Active Directory 樹系。

  - 沒有可用空間。

  - 在要求中使用無效的 SIP 標頭。

  - 已呼叫 Office Communications Server 2007 R2 伺服器或 Lync Server 伺服器。

  - 已停用 UM IP 閘道器。

  - 接聽電話之使用者的 URI 無效。

當 UM 疑難排解工具用於跨部門部署工具時，可回報的錯誤如下：

  - 並未啟用整合通訊的使用者。

  - 已停用 UM IP 閘道器。

  - 使用者的 URI 無效。

  - 安全性類型不符合 UM 撥號對應表。

  - 在要求中使用無效的 SIP 標頭。

  - 找不到 UM IP 閘道、撥號對應表或群組搜尋資訊。

UM 疑難排解工具會傳送一段時間為 15 秒的樣本 .wav 檔案。傳送及播放音訊檔案及 RTP 音訊資料流後，工具會回報一般音訊品質度量，以診斷與網路連線能力相關的音訊品質問題，例如抖動及平均封包遺失。這些報告包含往來 UM 伺服器的媒體資料流品質，並包含以下：

  - 網路平均意見分數 (NMOS)

  - 轉碼器

  - 延遲毫秒數 (ms)

  - 抖動毫秒數 (ms)

  - 封包遺失百分比

  - 要用於判斷音訊品質的 NMOS 分類及分級為：
    
      - NMOS 小於 2 = 差
    
      - NMOS 大於 2 但小於 3 = 中等
    
      - NMOS 大於 3 但小於 4 = 好
    
      - NMOS 大於 4 但小於 5 = 極佳

UM 疑難排解工具支援測試使用「安全」、「SIP 安全」及「非安全」呼叫的 UM 撥號對應表。如果您選擇「安全」或「SIP 安全」，則會檢查使用憑證的摘要，以判斷憑證是否到期，以及用於 TLS (傳輸層安全性) 通訊的憑證類型。憑證是用於正確識別及確認遠端電腦的身分。選取「安全」或「SIP 安全」模式時，UM 疑難排解工具會驗證下列是否為真：

  - 在本機電腦儲存區中找到本機憑證。

  - 使用的憑證可信任。

  - 在憑證中指定的目標名稱為有效。

  - 憑證已過期。

  - 遠端電腦信任憑證。

  - 憑證已撤銷。

  - 憑證沒有必要的增強金鑰使用方法。

UM 疑難排解工具可在「閘道」或 SIPClient 模式下執行，視有無部署 Office Communications Server 2007 R2 或 Lync Server 而定，或視 VoIP 閘道和 PBX 或 IP PBX 有無搭配 Unified Messaging Server 使用而定。使用「閘道」或 SIPClient 模式時，UM 疑難排解工具會支援使用下列格式的撥接電話。使用的格式需視 UM 撥號對應表的 URI 類型而定：

  - 電話分機 425-555-1010

  - E.164 電話號碼 +1 (425) 555-1010

  - SIP 位址 tonysmith@contoso.com

使用 SIPClient 模式時，UM 疑難排解工具會撥打語音備忘呼叫。這是一通不會使電話或整合通訊 (UC) 端點響起的呼叫，而會直接撥號到語音信箱。在 SIPClient 模式下執行 UM 疑難排解工具時，會決定：

  - 接聽的目標使用者。

  - 是否成功建立 SIP 呼叫。

  - Exchange 2010 Unified Messaging Server 或 Exchange 2013 Mailbox Server 是否接受 SIP 呼叫。

  - 是否接收正確的 DTMF 序列。

  - Exchange 2010 UM 伺服器或 Exchange 2013 Mailbox Server 是否有傳送與接收診斷的 .wav 檔案。

  - 媒體或音訊品質資料流收到時使用的計量。

UM 疑難排解工具會模擬來電，並執行一系列有助於內部管理員及租用戶系統管理員之自動答錄服務及識別組態錯誤測試呼叫流程的診斷測試。雖然 UM 疑難排解工具可用於自動答錄服務的案例，但無法用於測試下列類型的呼叫：

  - Outlook 語音存取呼叫，包括存取語音信箱、電子郵件、行事曆、目錄、個人通訊錄或個人選項的呼叫

  - UM 自動語音應答

  - 在電話上播放

  - 自動答錄服務規則

  - 傳真

  - 提示佈建

回到頁首

## UM 疑難排解架構

UM 疑難排解工具不僅可協助您疑難排解、診斷以及修復跨部門部署的組態問題，並可用於內部整合通訊部署。在跨部門部署中，此工具也可驗證站上 SBC 組態。管理員可測試整合通訊使用的所有整合通訊元件，包含 SBC。

## VoIP 閘道和 IP PBX 部署

在下列範例中，「閘道」模式可用來在不含 Office Communications Server 2007 R2 或 Lync Server 的環境中測試呼叫流程。此範例會測試電話語音設備，包括 VoIP 閘道、PBX、IP PBX 及整合通訊元件。此範例會將 VoIP 設定為「非安全」，並將 IP 位址 10.1.1.1 用做下一個躍點，且在轉接資訊中包含分機號碼。

    Test-ExchangeUMCallFlow -Mode Gateway -VoIPSecurity Unsecured -NextHop 10.1.1.1 -Diversion 12345

回到頁首

## Office Communications Server 2007 R2 和 Microsoft Lync Server 部署

UM 疑難排解工具可在設定 SIPClient 模式時，用於包含 Office Communications Server 2007 R2 或 Microsoft Lync Server 的內部或跨部門部署。下列範例會使用 SIPClient 模式，並在包含 Office Communications Server 2007 R2 或 Lync Server 伺服器的環境中，使用安全的 UM 撥號對應表來測試呼叫流程。依預設，在您執行 UM 疑難排解工具時，該工具會使用目前登入電腦之使用者的認證。當您執行下列範例時，會提示您輸入執行 UM 疑難排解工具時想使用的憑證。如需詳細資訊，請參閱[設定 Exchange UM 疑難排解工具搭配使用的認證](set-the-credentials-to-use-with-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)。

    Test-ExchangeUMCallFlow -Mode SIPClient -VoIPSecurity Secured -CallingParty tony@contoso.com -CalledParty david@contoso.com -Credential $get

## 安裝 UM 疑難排解工具

UM 疑難排解工具可安裝在執行下列作業系統的本機整合通訊伺服器上或其他 64 位元電腦上：

  - Windows 7 或 Windows 8 作業系統。

  - Windows Server 2008 或 Windows Server 2008 R2 作業系統。

  - Windows Server 2012 或 Windows Server 2012 R2 作業系統。

如果您要在 64 位元版的 Windows 7、Windows 8 或 64 位元版的 Windows Server 2008 上使用 UM 疑難排解工具，則在安裝 UM 疑難排解工具之前，您必須先安裝下列元件：

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1) 請參閱[Microsoft.NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果Windows Vista或Windows Server 2008電腦上執行此工具，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=178998">Windows Vista x64、 和 Windows Server 2008 x64 的 Microsoft.NET Framework 3.5 Family 更新</a>。</td>
    </tr>
    </tbody>
    </table>


  - Windows 遠端管理 (WinRM) 2.0 和 Windows PowerShell V2 (Windows6.0-KB968930.msu)   請參閱 Microsoft 知識庫文章 968930 [Windows 管理架構核心封裝 (Windows PowerShell 2.0 和 WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。

  - Microsoft Unified Communications Managed API 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi) 請參閱[Unified 的 Communications Managed API 2.0 Core Runtime （64 位元）](https://go.microsoft.com/fwlink/p/?linkid=198175)。

UM 疑難排解工具 (**Test-ExchangeUMCallFlow** cmdlet) 不包含在Exchange 2010 SP1 DVD、 僅包含Exchange 2010或 Exchange 2013 安裝媒體下載。但是您可以從[Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?linkid=182625)下載 UM 疑難排解工具。

如需詳細資訊，請參閱[安裝 Exchange UM 疑難排解工具](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)。

回到頁首

## Cmdlet 參數

下表包含可與 **Test-ExchangeUMCallFlow** 指令程式共用的參數，以及這些參數的說明。您也可使用「命令介面」命令 `Get-help Test-ExchangeUMCallFlow -detailed` 來尋找每個可與 **Test-ExchangeUMCallFlow** 指令程式共用的參數詳細資訊，以及使用方法範例。

### 參數

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>CalledParty</em></p></td>
<td><p><em>CalledParty</em> 參數可指定已啟用 Enterprise Voice 之 Office Communications Server 2007 R2 或 Lync Server 使用者的 SIP URI。這是 <strong>Test-ExchangeUMCallFlow</strong> 指令程式要撥打語音呼叫的使用者，例如：<code>-CalledParty tonysmith@contoso.com</code>。如果您在 SIPClient 模式下執行工具，請使用此參數。</p></td>
</tr>
<tr class="even">
<td><p><em>CallingParty</em></p></td>
<td><p><em>CallingParty</em> 參數可指定已啟用 Enterprise Voice 之 Office Communications Server 2007 R2 或 Lync Server 使用者的 SIP URI。這是撥接來電的使用者，例如：<code>-CallingParty tonysmith@contoso.com</code>。如果您在 SIPClient 模式下執行工具，請使用此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>Diversion</em></p></td>
<td><p><em>Diversion</em> 參數可指定應作為來電之轉接資訊進行傳送的字串。該字串可以是 Diversion 或 History-Info 標頭形式。來電包含的轉接資訊可以是分機號碼，也可以包含其他轉接資訊。</p>
<p>當您提供轉接資訊當作 History-Info 標頭時，請確認下列事項：</p>
<ul>
<li><p>不同的使用者部分至少有兩個不同項目。</p></li>
<li><p>最後一個項目會包含使用者的相關聯 UM 撥號對應表的整合通訊總機號碼。</p></li>
<li><p>倒數第二個項目包含已啟用 UM 的使用者的分機號碼。此項目也必須包含適當的原因文字。此文字必須根據標準 URL 參數逸出規則適當地逸出。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p><em>Mode</em> 參數可指定要使用 VoIP 閘道、IP PBX 還是 Office Communications Server 2007 R2 或 Lync Server 模式。如果您的 UM 部署包含 VoIP 閘道或 IP PBX，則可指定閘道模式，如果您的 UM 部署包含 Office Communications Server 2007 R2 或 Lync Server，則可指定 SIPClient 模式。</p></td>
</tr>
<tr class="odd">
<td><p><em>NextHop</em></p></td>
<td><p><em>NextHop</em> 參數可指定下個躍點的 IP 位址或完整網域名稱 (FQDN)，也可包括模擬 VoIP 閘道或 IP PBX 時，<strong>Test-ExchangeUMCallFlow</strong> Cmdlet 必須與其連線之下個躍點的 TCP 通訊埠。包含 TCP 通訊埠時，必須指定通訊埠 5060 (如果是「非安全」模式) 或通訊埠 5061 (如果是「安全」或「SIP 安全」模式)。例如：<code>gateway.contoso.com:5061</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateThumbprint</em></p></td>
<td><p><em>CertificateThumbprint</em> 參數可指定 TLS 所用憑證的指紋。不論在 UM 撥號對應表上設定「SIP 安全」或「安全」模式，這都是必要的。此憑證指紋是指從 VoIP 閘道、IP PBX 或 SBC 匯出的憑證。此外，已安裝 UM 疑難排解工具且正用於測試呼叫流程的電腦必須信任憑證授權單位為下一個躍點發出的憑證。</p></td>
</tr>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p><em>Credential</em> 參數可指定將用於執行指令程式的認證。</p></td>
</tr>
<tr class="even">
<td><p><em>HuntGroup</em></p></td>
<td><p><em>HuntGroup</em> 參數可指定與正在模擬之 VoIP 閘道相關聯的 UM 群組搜尋。這通常是分機號碼。如果您在「閘道」模式下執行工具，請使用此參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>VoIPSecurity</em></p></td>
<td><p><em>VoIPSecurity</em> 參數可指定在「閘道」 模式中使用指令程式時的安全性模式。您可以使用下列其中一種 VoIP 安全性模式：</p>
<ul>
<li><p>安全 (TLS/SRTP)</p></li>
<li><p>非安全 (TCP/RTP) (預設值)</p></li>
<li><p>SIP 安全 (TLS/RTP)</p></li>
</ul></td>
</tr>
</tbody>
</table>


回到頁首

