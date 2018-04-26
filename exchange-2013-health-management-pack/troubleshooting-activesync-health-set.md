---
title: 疑難排解 ActiveSync 健康情況設定
TOCTitle: 疑難排解 ActiveSync 健康情況設定
ms:assetid: 8a0b8b26-b4ef-41b8-8f71-8271c1735a69
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.activesync(v=EXCHG.150)
ms:contentKeyID: 53276408
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 ActiveSync 健康情況設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Exchange ActiveSync健全設定監視ActiveSync服務您組織中的行動用戶端的整體狀況。下列的健全設定密切相關ActiveSync健全設定：

[疑難排解 ActiveSync.Protocol 健全設定](troubleshooting-activesync-protocol-health-set.md)

[疑難排解 ActiveSync.Proxy 健全設定](troubleshooting-activesync-proxy-health-set.md)

如果您收到警示，指出 ActiveSync 健全設定的狀況不良，表示可能有問題令使用者無法使用 ActiveSync 來存取信箱。

## 說明

ActiveSync 服務是透過下列探查與監視器受到監視。


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
<td><p>ActiveSyncCTPProbe</p></td>
<td><p>ActiveSync</p></td>
<td><p>Active Directory</p>
<p>驗證</p>
<p>Mailbox Server 驗證</p>
<p>資訊儲存庫</p>
<p>高可用性</p>
<p>網路</p></td>
<td><p>ActiveSyncCTPMonitor (ActiveSync 健全設定)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncProxyTestProbe</p></td>
<td><p>ActiveSync.Proxy</p></td>
<td><p>-</p></td>
<td><p>ActiveSyncProxyTestMonitor (ActiveSync.Proxy 健全設定)</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSyncDeepTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>驗證</p>
<p>資訊儲存庫</p>
<p>高可用性</p></td>
<td><p>ActiveSyncDeepTestMonitor (ActiveSync 健全設定)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncSelfTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>驗證</p></td>
<td><p>ActiveSyncSelfTestMonitor (ActiveSync.Protocol 健全設定)</p>
<p>RequestsQueuedGt500Monitor (ActiveSync 健全設定)</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 使用者動作

有可能服務復原之後則發出警示。因此，當您會收到通知，指定ActiveSync健全設定為不健康，先確認問題仍然存在。如果問題不存在，執行下列各節所述的適當的復原動作。

## 確認問題

1.  識別警示中提供的健全設定名稱與伺服器名稱。

2.  郵件的詳細資訊提供的確切原因的警示的資訊。在大多數情況下，郵件詳細資料會提供足夠來協助識別根本原因的疑難排解資訊。如果不清楚郵件的詳細資訊，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取 server1.contoso.com 的 ActiveSync 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ActiveSync"}
    
    2.  檢閱命令的輸出傳送至決定顯示器回報的錯誤。發出警示監視器**AlertValue**值會是**Unhealthy**。
    
    3.  請為不健康狀態監視重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**ActiveSyncCTPMonitor**。相關聯的監視探查是**ActiveSyncCTPProbe**。若要執行此探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe ActiveSync\ActiveSyncCTPProbe -Server server1.contoso.com | Format-List
    
    4.  命令輸出中，請檢閱"結果 」 一節的探查。如果值為**成功**，問題是暫時性錯誤，並不存在。否則，請參閱下列各節所述的復原步驟。

## ActiveSyncDeepTestMonitor 和 ActiveSyncSelfTestMonitor 復原動作

這個監視器警示通常會發出 Mailbox server 上。若要執行復原動作，請遵循下列步驟：

1.  啟動 IIS 管理員中，並再連線到回報問題的伺服器。按一下 \[**應用程式集區**，然後再回收已命名**MSExchangeSyncAppPool**ActiveSync 應用程式集區。

2.  依照Verifying the issue一節中的步驟 2c，重新執行相關聯的探查。

3.  如果問題仍然存在，請使用 IISReset 公用程式來回收整個 IIS 服務。

4.  依照Verifying the issue一節中的步驟 2c，重新執行相關聯的探查。

5.  如果問題仍然存在，重新啟動伺服器。若要這樣做，第一個容錯移轉資料庫的伺服器上裝載使用下列命令：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    在此範例和所有後續程式碼範例中，以實際伺服器名稱取代 *server1.contoso.com*。

6.  接下來，確認移動所有資料庫成功關閉回報問題的伺服器。若要這樣做，執行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status

7.  如果在步驟 6 中的命令輸出顯示伺服器上沒有主動副本，重新啟動伺服器。如果輸出沒有顯示主動副本，請再次執行步驟 5 與 6。

8.  伺服器重新啟動後，請依照Verifying the issue一節中的步驟 2c，重新執行相關聯的探查。

9.  如果探查成功，請執行下列命令來容錯移轉資料庫：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

10. 如果探查仍失敗，您可能需要進一步取得協助若要解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## ActiveSyncCTPMonitor 復原動作

此監視器警示通常是在 CA 伺服器 (CAS) 上發出。

1.  啟動 IIS 管理員中，並再連線到回報問題的伺服器。按一下 \[**應用程式集區**，並再回收名為**MSExchangeSyncAppPool**ActiveSync應用程式集區。

2.  依照Verifying the issue一節中的步驟 2c，重新執行相關聯的探查。

3.  如果問題仍然存在，請使用 IISReset 公用程式來回收整個 IIS 服務。

4.  依照Verifying the issue一節中的步驟 2c，重新執行相關聯的探查。

5.  如果問題持續發生，您必須先確認對應的信箱伺服器上的健康狀態。信箱伺服器的名稱是錯誤訊息中所指定的`_Mbx:`值。
    
    1.  執行下列命令以取得適當的信箱伺服器。例如，執行下列命令名為 mailbox1.contoso.com Mailbox server：
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "ActiveSync*"}
    
    2.  如果任一命令輸出中所列的監視器報告為不健康，必須先解決這些監視器。若要這樣做，請遵循ActiveSyncDeepTestMonitor 與 ActiveSyncSelfTestMonitor 復原動作\] 區段中所述的疑難排解步驟。

6.  如果 Mailbox Server 上的所有監視器都狀況良好，請重新啟動 CAS。

7.  伺服器重新啟動後，請依照Verifying the issue一節中的步驟 2c，重新執行相關聯的探查。

8.  如果探查持續失敗，您可能需要進一步取得協助若要解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## RequestsQueuedGt500Monitor 復原動作

此監視器警示通常是在 CA 伺服器上發出。

1.  啟動 IIS 管理員中，並再連線到回報問題的伺服器。按一下 \[**應用程式集區**，並再回收名為**MSExchangeSyncAppPool**ActiveSync應用程式集區。

2.  等候 10 分鐘，以查看是否仍狀況良好監視器。在 10 分鐘後執行下列命令以取得適當的伺服器。例如，執行下列命令以取得 server1.contoso.com:
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "ActiveSync*"}

3.  如果問題仍然存在，請使用 IISReset 公用程式來回收整個 IIS 服務。

4.  等待 10 分鐘，然後重新執行步驟 2 中顯示的命令，查看監視器是否仍然狀況良好。

5.  如果問題持續發生，重新啟動伺服器。CAS 伺服器時，只會重新啟動伺服器。信箱伺服器之伺服器時，請執行下列動作：
    
    1.  容錯移轉伺服器裝載的資料庫。若要這樣做，執行下列命令：
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **附註**   在這個及所有後續程式碼範例中，請將 *server1.contoso.com* 取代為實際的伺服器名稱。
    
    2.  確認所有資料庫都已搬離回報問題的伺服器。若要執行此動作，請執行下列命令：
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        如果命令輸出顯示伺服器上沒有主動副本，請重新啟動伺服器。

6.  伺服器重新啟動之後，等待 10 分鐘，然後重新執行步驟 2 中顯示的命令，判斷監視器是否仍然狀況良好。

7.  如果監視器仍然狀況良好，且這是 Mailbox Server，則執行下列命令來容錯移轉資料庫：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

8.  如果探查持續失敗，您可能需要進一步取得協助若要解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange ActiveSync](https://technet.microsoft.com/zh-tw/library/aa998357\(v=exchg.150\))

[行動裝置](https://technet.microsoft.com/zh-tw/library/bb232129\(v=exchg.150\))

[Exchange ActiveSync 虛擬目錄的管理工作](https://technet.microsoft.com/zh-tw/library/bb125170\(v=exchg.150\))

