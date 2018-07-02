---
title: 疑難排解 EWS 健全設定
TOCTitle: 疑難排解 EWS 健全設定
ms:assetid: f5aaacdd-7f4a-4d63-8440-1c564e644dfc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.ews(v=EXCHG.150)
ms:contentKeyID: 53276421
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 EWS 健全設定

 

_**適用版本：** Exchange Server 2013, Project Server 2013_

_**上次修改主題的時間：** 2015-03-09_

Exchange Web 服務 (EWS) 健全設定會監視 EWS 服務的整體健康狀況。EWS 健全設定與下列健全設定密切相關：

[疑難排解 EWS。通訊協定健全設定](troubleshooting-ews-protocol-health-set.md)

[疑難排解 EWS。Proxy 健全設定](troubleshooting-ews-proxy-health-set.md)

如果您收到警示，指出 EWS 的狀況不良，表示可能有問題令使用者無法與 Exchange 伺服器通訊。

## 說明

EWS 是透過下列探查與監視器受到監視。


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
<td><p>EwsCtpProbe</p></td>
<td><p>EWS</p></td>
<td><p>資訊儲存庫</p>
<p>Active Directory 網域服務 (AD DS)</p></td>
<td><p>EwsCtpMonitor (EWS 健全設定)</p></td>
</tr>
<tr class="even">
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory 網域服務 (AD DS)</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="odd">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>資訊儲存庫</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


此探查會使用監視帳戶，執行從 Client Access Server (CAS) 到 Mailbox Server 的完整 EWS 登入。此探查會在 EWS 上呼叫 **GetFolder** 方法。如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 常見問題

下列任一常見原因都可能導致此探查失敗：

  - 探查使用的驗證機制與 CAS 虛擬目錄上使用的驗證機制不符。

  - 受監視 CAS 中的 EWS 應用程式集區沒有回應。

  - CAS 連線到 Mailbox Server 時發生網路問題。

  - CAS 連線到網域控制站時發生通訊問題。

  - 網域控制站無回應。

  - 位於一或多個 Mailbox Server 上的 EWS 應用程式集區沒有回應。

  - 未裝載使用者的資料庫，或特定信箱無法使用資訊儲存庫。

  - 一或多個 Mailbox Server 上的 Information Store 服務發生問題。

## 使用者動作

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。
    
    當您收到來自此健全設定的警示時，電子郵件會包含下列資訊：
    
    1.  產生警示之 CAS 的名稱
    
    2.  被探查當成目標資源來監視之 Mailbox Server 的名稱
    
    3.  上一個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊
    
    4.  事件的發生時間
    
    5.  所使用的驗證機制及認證資訊
    
    例外狀況追蹤資訊可提供關於探查為何失敗的最重要線索。呈報訊息也包含下列 HTTP 標頭：
    
    1.  **X-FEServer**   指出執行探查的 CAS
    
    2.  **X-TargetBEServer**   指出要求被路由傳送到的 MBX 伺服器
    
    3.  **X-DiagInfo**   指出收到要求的 MBX 伺服器

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取 server1.contoso.com 的 EWS 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  為狀況不良的監視器重新執行相關聯的探查。請參閱Explanation一節中的表格，以找出相關聯的探查。若要執行此動作，請執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        對於 EWS 健全設定，假設失敗的監視器是 **EWSCtpMonitor**。與該監視器相關聯的探查為 **EWSCtpProbe**。若要在 server1.contoso.com 上執行該探查，請執行下列命令：
        
            Invoke-MonitoringProbe EWS\EWSCtpProbe -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## EwsCtpMonitor 復原動作

1.  啟動 \[IIS 管理員\]，然後連線到回報問題的伺服器，以判斷 CAS 和 Mailbox Server 上是否都在執行 **MSExchangeServicesAppPool** 應用程式集區。

2.  找出探查失敗的 MailboxDatabase。確認 Mailbox Server 的信箱資料庫在使用中，且資訊儲存庫的狀況良好。

3.  按一下 **\[應用程式集區\]**，然後在命令介面中執行下列命令，以重複使用 **MSExchangeServicesAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

5.  如果問題仍然存在，請使用 IISReset 公用程式來回收整個 IIS 服務。

6.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

7.  如果問題仍然存在，請檢閱 CA 和 Mailbox Server 上的通訊協定記錄檔。CAS 的通訊協定記錄會位於 *\<Exchange Server 安裝目錄\>\\Logging\\HttpProxy\\Ews* 資料夾中。在 Mailbox Server 上，這些記錄會位於 *\<Exchange Server 安裝目錄\>\\Logging\\Ews* 資料夾中。

8.  建立測試使用者帳戶，然後對指定的 CAS 執行測試使用者帳戶來進行登入。例如，若要登入，可使用：https://\<servername\>/ews/exchange.asmx。如果問題仍然存在，請試試其他 CAS，以判斷問題是否出在 CAS，而不是 Mailbox Server。如果測試使用者名稱通過驗證，則問題可能出在特定的信箱資料庫或該監視信箱所在的 Mailbox Server。使用信箱資料庫中存在的測試帳戶，嘗試重複此步驟。

9.  檢查 CA 與 Mailbox Server 之間的網路連線。

10. 檢查 EWS.Proxy 健全設定上是否有任何警示可能指出有問題影響特定的 CAS。

11. 檢查 EWS.Protocol 健全設定上是否有任何警示可能指出有問題影響特定的 Mailbox Server。

12. 如果問題仍然存在，請重新啟動伺服器。若要這樣做，請先容錯移轉伺服器上裝載的資料庫。若要執行此動作，請執行下列命令：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    **附註**   在這個及所有後續程式碼範例中，請將 *server1.contoso.com* 取代為實際的伺服器名稱。

13. 確認所有資料庫都已搬離回報問題的伺服器。若要執行此動作，請執行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    如果命令輸出顯示伺服器上沒有主動副本，請重新啟動伺服器。

14. 伺服器重新啟動後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

15. 如果探查成功，請執行下列命令來容錯移轉資料庫回到 Mailbox Server：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

16. 如果探查持續失敗，請尋求協助以解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

