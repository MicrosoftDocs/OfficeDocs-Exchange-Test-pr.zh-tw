---
title: 疑難排解 EWS。通訊協定健全設定
TOCTitle: 疑難排解 EWS。通訊協定健全設定
ms:assetid: 826b2d5b-adbb-4bf5-94b6-0a8de2e3aac0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.ews.protocol(v=EXCHG.150)
ms:contentKeyID: 53276406
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 EWS。通訊協定健全設定

 

_**適用版本：**Exchange Server 2013, Project Server 2013_

_**上次修改主題的時間：**2015-03-09_

EWS。通訊協定健全設定監視Exchange Mailbox server 上的 Web 服務 (EWS) 通訊協定。EWS。下列的健全設定密切相關通訊協定健全設定：

[疑難排解 EWS 健全設定](troubleshooting-ews-health-set.md)

[疑難排解 EWS。Proxy 健全設定](troubleshooting-ews-proxy-health-set.md)

如果您收到的警示指出 EWS.Protocol 的狀況不良，這表示讓使用者無法存取 Exchange 的問題。

## 說明

EWS.Protocol 健全設定是由下列探查所組成：

1.  EwsSelfTestProbe

2.  EwsDeepTestProbe

EwsSelfTestProbe 不會根據資訊儲存庫。不過，EwsDeepTestProbe 探查資訊儲存庫而定。這兩個這些探查執行 Mailbox server 上的 EWS 作業以及他們為用戶端存取伺服器 (CAS) 使用相同的驗證方法。EwsSeftTestProbe 呼叫**ConvertId**方法，並 EwsDeepTestProbe 呼叫**GetFolder**方法。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>健全設定</th>
<th>相依性</th>
<th>關聯的監視器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>資訊儲存庫</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

當您接收來自此 HealthSet 的警示時，郵件會包含下列資訊：

1.  產生警示的 Mailbox Server 名稱

2.  最後一項錯誤的完整例外狀況追蹤，包含診斷資料和特定 HTTP 標頭資訊

3.  事件的發生時間

## 常見問題

下列任一常見原因都可能導致此探查失敗：

  - 受監視 Mailbox Server 上的 EWS 應用程式集區無法正常運作。

  - 網域控制站無回應，或無法與 Mailbox Server 通訊。

  - 使用者的資料庫並未裝載，或 Information Store 無法使用於特定信箱。

## 使用者動作

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取關於 server1.contoso.com 的 EWS.Protocol 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Protocol"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  請為不健康狀態監視重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**EWSSelfTestMonitor**。相關聯的監視探查是**EWSSelfTestProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe EWS.Protocol\EWSSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## EWSSelfTestMonitor 和 EWSDeepTestMonitor 復原動作

此監視器警示通常是針對 Mailbox Server 發出。

1.  啟動 IIS Manager，然後連接至回報問題的伺服器，以判斷 MSExchangeServicesAppPool 是否同時在 CA 和 Mailbox Server 上執行。

2.  找出失敗探查的 MailboxDatabase，然後確認 MailboxDatabase 適用於 MailboxServer，而且 Information Store 的狀況良好。

3.  按一下 **\[應用程式集區\]**，然後在命令介面中執行下列命令，以重複使用 **MSExchangeServicesAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  重新執行關聯的探查，如Verifying the issue still exists一節的步驟 2c 所示。

5.  如果問題仍然存在，請利用 IISReset 公用程式，重新啟動 IIS 服務。

6.  重新執行關聯的探查，如Verifying the issue still exists一節的步驟 2c 所示。

7.  如果問題仍然結束，請檢閱通訊協定記錄檔的 Mailbox server 上。在信箱伺服器上，記錄檔位於*\<exchange server installation directory\>*\\Logging\\Ews 資料夾中。

8.  建立測試使用者帳戶，並再登入所使用的測試使用者帳戶針對指定的信箱伺服器上的連接埠 444 https://*\<servername\>*: 444/ews/exchange.asmx。如果測試成功，發生問題可能會影響特定的信箱資料庫或監控信箱所在的 Mailbox server。嘗試使用該資料庫上的測試帳戶重複此步驟。

9.  檢查 EWS.Protocol 健全設定上可能表示會影響特定 Mailbox Server 之問題的任何警示。

10. 如果問題仍然存在，重新啟動伺服器。若要這樣做，第一個容錯移轉資料庫伺服器上裝載使用下列命令：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    在此範例和所有後續程式碼範例中，以實際伺服器名稱取代 *server1.contoso.com*。

11. 確認所有資料庫都已搬離回報問題的伺服器。若要執行此動作，請執行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    如果命令輸出顯示伺服器上沒有主動副本，伺服器會儲存在重新啟動。重新啟動伺服器。

12. 重新啟動伺服器之後，重新執行關聯的探查，如Verifying the issue still exists一節的步驟 2c 所示。

13. 如果探查成功，請執行下列命令來容錯移轉資料庫：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

14. 如果探查持續失敗，請尋求協助以解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

