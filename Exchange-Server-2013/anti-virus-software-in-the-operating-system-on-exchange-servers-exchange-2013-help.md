---
title: 'Exchange Server 的作業系統中的防毒軟體: Exchange 2013 Help'
TOCTitle: Exchange Server 的作業系統中的防毒軟體
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 50473578
ms.date: 01/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 的作業系統中的防毒軟體

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-07-22_

本主題說明檔案等級防毒程式對執行 Microsoft Exchange Server 2013 之電腦的影響。如果您執行本主題中所述的建議，即可協助增強 Exchange 組織的安全性及健康情況。

檔案等級掃描程式是經常使用的掃描程式。然而，如果它們的設定不正確，可能會造成 Exchange 2013 問題。檔案等級掃描程式有兩種類型：

  - 「記憶體駐留檔案等級掃描」指的是隨時都載入在記憶體中的檔案等級防毒軟體部分。它會檢查硬碟及電腦記憶體中使用的所有檔案。

  - 「點播檔案等級掃描」指的是可以手動或設定排程來掃描磁碟上檔案的檔案等級防毒軟體部分。部分防毒軟體版本會在更新病毒碼之後自動啟動點播掃描，以確定使用最新的病毒碼來掃描所有檔案。

搭配使用檔案等級掃描程式與 Exchange 2013 時，可能會發生下列問題：

  - 檔案等級掃描程式會定期掃描檔案，或在要使用檔案時掃描檔案。這樣可能會導致當 Exchange 2013 嘗試使用檔案時，掃描程式卻鎖定或隔離 Exchange 記錄或資料庫檔案。此行為可能會造成 Exchange 2013 嚴重失敗，也可能會造成 -1018 事件日誌錯誤。

  - 檔案等級掃描程式不提供電子郵件病毒的保護，例如風暴蠕蟲 (Storm Worm)。風暴蠕蟲 (Storm Worm) 是透過電子郵件自行傳播的特洛伊木馬後門程式。該蠕蟲會將受感染的電腦加入殭屍網路 (Botnet)，然後利用該電腦以週期性突發方式傳送垃圾郵件。

## 搭配 Exchange 2013 使用檔案等級掃描的建議

如果在 Exchange 2013 伺服器上部署檔案等級掃描程式，請確定記憶體駐留及檔案層級掃描都設定了適當的排除項目，例如目錄排除、處理程序排除及副檔名排除。此節說明建議的的目錄排除、處理程序排除及副檔名排除。

**目錄**

目錄排除

處理程序排除

副檔名排除

## 目錄排除

您必須排除每部執行檔案等級防毒掃描程式之 Exchange 伺服器的特定目錄。本節說明應該排除不進行檔案等級掃描的目錄。

  - **信箱伺服器**
    
      - **信箱資料庫**
        
          - Exchange 資料庫、檢查點檔案及記錄檔。這些檔案預設是位在 %ExchangeInstallPath%Mailbox 資料夾的子資料夾中。若要判斷信箱資料庫、交易記錄及檢查點檔案的位置，請執行下列命令：`Get-MailboxDatabase -Server <servername>| Format-List *path*`
        
          - 資料庫內容索引。這些檔案預設是位在與資料庫檔案相同的資料夾中。
        
          - 群組計量檔案。這些檔案預設是位在 %ExchangeInstallPath%GroupMetrics 資料夾中。
        
          - 一般記錄檔，例如郵件追蹤和行事曆修復記錄檔。這些檔案預設是位在 %ExchangeInstallPath%TransportRoles\\Logs 資料夾及 %ExchangeInstallPath%Logging 資料夾的子資料夾中。若要判斷正在使用的記錄路徑，請在 Exchange 管理命令介面中執行下列命令：`Get-MailboxServer <servername> | Format-List *path*`
        
          - 離線通訊錄檔案。這些檔案預設是位在 %ExchangeInstallPath%ClientAccess\\OAB 資料夾的子資料夾中。
        
          - %SystemRoot%\\System32\\Inetsrv 資料夾中的 IIS 系統檔案。
        
          - 信箱資料庫暫存資料夾：%ExchangeInstallPath%Mailbox\\MDBTEMP
    
      - **資料庫可用性群組的成員**
        
          - 所有在 \[信箱資料庫\] 清單中列出的項目，與存於 %Windir%\\Cluster 的叢集仲裁資料庫。
        
          - 見證目錄檔案。這些檔案位於環境中的另一個伺服器，通常是並非安裝在同一台電腦作為信箱伺服器的用戶端存取伺服器。這些見證目錄檔案預設是位於 %SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\>。
    
      - **Transport 服務**
        
          - 記錄檔，例如，郵件追蹤和連線記錄檔。這些檔案預設是位在 %ExchangeInstallPath%TransportRoles\\Logs 資料夾的子資料夾中。若要判斷正在使用的記錄路徑，請在 Exchange 管理命令介面中執行下列命令：`Get-TransportService <servername> | Format-List *logpath*,*tracingpath*`
        
          - 收取和重新顯示郵件目錄資料夾。這些資料夾預設是位在 %ExchangeInstallPath%TransportRoles 資料夾下。若要判斷正在使用的路徑，請在 Exchange 管理命令介面中執行下列命令：`Get-TransportService <servername>| Format-List *dir*path*`
        
          - 佇列資料庫、檢查點及記錄檔。這些檔案預設是位在 %ExchangeInstallPath%TransportRoles\\Data\\Queue 資料夾中。
        
          - 寄件者信譽資料庫、檢查點和記錄檔。這些檔案預設是位在 %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation 資料夾中。
        
          - 用來執行轉換的暫存資料夾：
            
              - 內容轉換預設是在 Exchange 伺服器的 %TMP% 資料夾中執行。
            
              - RTF 格式到 MIME/HTML 的轉換預設是在 %ExchangeInstallPath%\\Working\\OleConverter 資料夾中執行。
        
          - 內容掃描元件是由惡意程式碼代理程式與資料外洩防護 (DLP) 功能所使用。這些檔案預設是位在 %ExchangeInstallPath%FIP-FS 資料夾中。
    
      - **Mailbox Transport 服務**
        
          - 記錄檔，例如，連線記錄檔。這些檔案預設是位在 %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox 資料夾的子資料夾中。若要判斷正在使用的記錄路徑，請在 Exchange 管理命令介面中執行下列命令：`Get-MailboxTransportService <servername> | Format-List *logpath*`
    
      - **整合通訊**
        
          - 不同地區設定的文法檔案，例如 en-EN 或 es-ES。這些檔案預設會儲存在 %ExchangeInstallPath%UnifiedMessaging\\grammars 資料夾的子資料夾中。
        
          - 語音提示、問候語和參考訊息檔案。這些檔案預設會儲存在 %ExchangeInstallPath%UnifiedMessaging\\Prompts 資料夾的子資料夾中。
        
          - 暫時儲存在 %ExchangeInstallPath%UnifiedMessaging\\voicemail 資料夾中的語音信箱檔案。
        
          - 由整合通訊產生的暫存檔案。這些檔案預設會儲存在 %ExchangeInstallPath%UnifiedMessaging\\temp 資料夾中。
    
      - **設定**
        
          - Exchange 伺服器設定暫存檔案。這些檔案通常位於 %SystemRoot%\\Temp\\ExchangeSetup。
    
      - **Exchange 搜尋服務**
        
          - 由 Exchange 搜尋服務和 Microsoft Filter Pack 所使用的暫存檔案，以在沙箱化環境中執行檔案轉換。這些檔案位於 %SystemRoot%\\Temp\\OICE\_*\<GUID\>*\\。

<!-- end list -->

  - **Client Access Server**
    
      - **網路元件**
        
          - 針對使用網際網路資訊服務 (IIS) 7.0 的伺服器，與 Microsoft Outlook Web App 搭配使用的壓縮資料夾。IIS 7.0 的壓縮資料夾預設是位在 %SystemDrive%\\inetpub\\temp\\IIS Temporary Compressed Files。
        
          - %SystemRoot%\\System32\\Inetsrv 資料夾中的 IIS 系統檔案
        
          - Inetpub\\logs\\logfiles\\w3svc
        
          - %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary ASP.NET 檔案中的子資料夾
    
      - **POP3 與 IMAP4 通訊協定記錄**
        
          - POP3 資料夾：%ExchangeInstallPath%Logging\\POP3
        
          - IMAP4 資料夾：%ExchangeInstallPath%Logging\\IMAP4
    
      - **Front End Transport 服務**
        
          - 記錄檔，例如，連線記錄與通訊協定記錄。這些檔案預設是位在 %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd 資料夾的子資料夾中。若要判斷正在使用的記錄路徑，請在 Exchange 管理命令介面中執行下列命令：`Get-FrontEndTransportService <servername> | Format-List *logpath*`
    
      - **設定**
        
          - Exchange 伺服器設定暫存檔案。這些檔案通常位於 %SystemRoot%\\Temp\\ExchangeSetup。

回到頁首

## 處理程序排除

許多檔案等級掃描程式現在支援處理程序的掃描，如果掃描不正確的處理程序，可能會對 Microsoft Exchange 造成負面影響。因此，您應該從檔案等級掃描程式中排除下列處理程序。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>程序</th>
<th>路徑</th>
<th>註解</th>
<th>伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dsamain.exe</p></td>
<td><p>%SystemRoot%\System32</p></td>
<td><p>已訂閱 Edge Transport Server 上的 Active Directory 輕量型目錄服務 (AD LDS)。</p></td>
<td><p>Edge Transport Server</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 傳輸服務工作者處理序</p></td>
<td><p>信箱伺服器</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="odd">
<td><p>fms.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>惡意程式碼代理程式與 DLP 功能所使用的內容掃描元件。</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>hostcontrollerservice.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\HostController</p></td>
<td><p>Microsoft Exchange 搜尋主機控制器服務 (HostControllerService)</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p></td>
</tr>
<tr class="odd">
<td><p>inetinfo.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.AntispamUpdateSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 反垃圾郵件更新服務 (MSExchangeAntispamUpdate)</p></td>
<td><p>信箱伺服器</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.ContentFilter.Wrapper.exe</p></td>
<td><p>%ExchangeInstallPath%TransportRoles\agents\Hygiene</p></td>
<td><p>內容篩選器代理程式</p></td>
<td><p>信箱伺服器</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Diagnostics.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 診斷服務 (MSExchangeDiagnostics)</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Directory.TopologyService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Active Directory 拓撲服務 (MSExchangeADTopology)</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.EdgeCredentialSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 憑證服務 (MSExchangeEdgeCredential)</p></td>
<td><p>Edge Transport Server</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.EdgeSyncSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange EdgeSync 服務 (MSExchangeEdgeSync)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Imap4.exe</p></td>
<td><p>ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 服務 (MSExchangeImap4)</p></td>
<td><p>Client Access Server</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Imap4service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 後端服務 (MSExchangeIMAP4BE)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Pop3.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange POP3 服務 (MSExchangePop3)</p></td>
<td><p>Client Access Server</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Pop3service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange POP3 後端服務 (MSExchangePOP3BE)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.ProtectedServiceHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 服務主機服務 (MSExchangeServiceHost)</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.RPCClientAccess.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange RPC 用戶端存取服務 (MSExchangeRPC)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Search.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 搜尋服務 (MSExchangeFastSearch)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Servicehost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 服務主機服務 (MSExchangeServiceHost)</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Store.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Information Store Service (MSExchangeIS)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Store.Worker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Information Store Service 工作者處理序</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.UM.CallRouter.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\CallRouter</p></td>
<td><p>Microsoft Exchange 整合通訊呼叫路由器服務 (MSExchangeUMCR)</p></td>
<td><p>Client Access Server</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeDagMgmt.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange DAG 管理服務 (MSExchangeDagMgmt)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeDelivery.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 信箱傳輸傳遞服務 (MSExchangeDelivery)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeFrontendTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 前端傳輸服務 (MSExchangeFrontEndTransport)</p></td>
<td><p>Client Access Server</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeHMHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 健康情況管理員服務 (MSExchangeHM)</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeHMWorker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 健康情況管理員服務工作者處理序</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 信箱助理員服務 (MSExchangeMailboxAssistants)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxReplication.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 信箱複寫服務 (MSExchangeMailboxReplication)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMigrationWorkflow.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 移轉工作流程服務 (MSExchangeMigrationWorkflow)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeRepl.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 複寫服務 (MSExchangeRepl)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeSubmission.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 信箱傳輸提交服務 (MSExchangeSubmission)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 傳輸服務 (MSExchangeTransport)</p></td>
<td><p>信箱伺服器</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeTransportLogSearch.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 傳輸記錄搜尋服務 (MSExchangeTransportLogSearch)</p></td>
<td><p>信箱伺服器</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeThrottling.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 節流服務 (MSExchangeThrottling)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>Noderunner.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0</p></td>
<td><p>Microsoft Exchange 搜尋服務 (MSExchangeFastSearch)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>OleConverter.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>針對外部收件者將 RTF 格式 (RTF) 郵件轉換為 MIME/HTML。</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>ParserServer.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\ParserServer</p></td>
<td><p>Microsoft Exchange 搜尋服務 (MSExchangeFastSearch)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>Powershell.exe</p></td>
<td><p>C:\Windows\System32\WindowsPowerShell\v1.0</p></td>
<td><p>Exchange 管理命令介面</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p>
<p>Edge Transport Server</p></td>
</tr>
<tr class="even">
<td><p>ScanEngineTest.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>惡意程式碼代理程式與 DLP 功能所使用的內容掃描元件。</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>ScanningProcess.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>惡意程式碼代理程式與 DLP 功能所使用的內容掃描元件。</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>TranscodingService.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing</p></td>
<td><p>Outlook Web App 中的 WebReady 文件檢視。</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>UmService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 整合通訊服務 (MSExchangeUM)</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>UmWorkerProcess.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 整合通訊服務工作者處理序</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="odd">
<td><p>UpdateService.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>惡意程式碼代理程式與 DLP 功能所使用的內容掃描元件。</p></td>
<td><p>信箱伺服器</p></td>
</tr>
<tr class="even">
<td><p>W3wp.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet Information Services (IIS)</p></td>
<td><p>信箱伺服器</p>
<p>Client Access Server</p></td>
</tr>
</tbody>
</table>


回到頁首

## 副檔名排除

除了排除特定的目錄和處理程序外，還應該排除下列 Exchange 特定副檔名，以防目錄排除失敗或從檔案的預設位置移動檔案。

  - 應用程式相關的副檔名：
    
      - .config
    
      - .dia
    
      - .wsb

<!-- end list -->

  - 資料庫相關的副檔名：
    
      - .chk
    
      - .edb
    
      - .jrs
    
      - .jsl
    
      - .log
    
      - .que

<!-- end list -->

  - 離線通訊錄相關的副檔名：
    
      - .lzx

<!-- end list -->

  - 內容索引相關的副檔名：
    
      - .ci
    
      - .dir
    
      - .wid
    
      - .000
    
      - .001
    
      - .002

<!-- end list -->

  - 整合通訊相關的副檔名：
    
      - .cfg
    
      - .grxml

<!-- end list -->

  - 群組計量相關的副檔名：
    
      - .dsc
    
      - .txt

回到頁首

