---
title: 疑難排解 IMAP 健全設定
TOCTitle: 疑難排解 IMAP 健全設定
ms:assetid: 2a06e671-4cc2-4ce5-bf53-6243ea140f20
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.imap(v=EXCHG.150)
ms:contentKeyID: 53276399
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 IMAP 健全設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

IMAP 健全設定監視用戶端存取伺服器 (CAS) 上的 IMAP4 proxy 基礎結構的可用性。下列的健全設定密切相關之 IMAP 健全設定：

[疑難排解 IMAP。通訊協定健全設定](troubleshooting-imap-protocol-health-set.md)

[疑難排解 IMAP。Proxy 健全設定](troubleshooting-imap-proxy-health-set.md)

如果您收到警示，指出 IMAP 不健康，這表示發生問題，可能導致使用者無法使用 IMAP 來存取他們的信箱。

## 說明

IMAP4 服務的監視可以使用下列探查和監視器。


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
<td><p>ImapCTPProbe</p></td>
<td><p>IMAP</p></td>
<td><p>Active Directory</p>
<p>驗證</p>
<p>Mailbox Server 驗證</p>
<p>高可用性</p>
<p>網路功能</p></td>
<td><p>ImapCTPMonitor (IMAP 健全設定)</p></td>
</tr>
<tr class="even">
<td><p>ImapProxyTestProbe</p></td>
<td><p>IMAP.Proxy</p></td>
<td><p>Active Directory</p>
<p>驗證</p></td>
<td><p>ImapProxyTestMonitor (IMAP.Proxy 健全設定)</p></td>
</tr>
<tr class="odd">
<td><p>ImapDeepTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>驗證</p>
<p>資訊儲存庫</p>
<p>高可用性</p></td>
<td><p>IMAP.Protocol (IMAP.Protocol 健全設定)</p></td>
</tr>
<tr class="even">
<td><p>ImapSelfTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>驗證</p></td>
<td><p>IMAP.Protocol (IMAP.Protocol 健全設定)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (IMAP 健全設定)</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 使用者動作

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取關於 server1.contoso.com 的 IMAP 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  處於不健全的狀態監視器，重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**ImapCTPMonitor**。相關聯的監視探查是**ImapCTPProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe IMAP\ImapCTPProbe -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## ImapTestDeepMonitor 和 ImapSelfTestMonitor 復原動作

1.  重新啟動Exchange後端伺服器上的 IMAP4 服務。如需如何停止及啟動 IMAP4 服務的詳細資訊，請參閱[啟動及停止 IMAP4 服務](https://technet.microsoft.com/zh-tw/library/bb124022\(v=exchg.150\))。

2.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

3.  如果問題仍然存在，您必須使用下列命令來容錯移轉由 Mailbox Server 主控的資料庫：
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  確認已移動所有資料庫成功關閉回報問題的伺服器。若要這樣做，執行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    如果命令輸出顯示伺服器上沒有主動副本，請重新啟動伺服器。

5.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

6.  如果探查成功，請執行下列命令來容錯移轉資料庫：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## ImapCTPMonitor 復原動作

此監視器警示通常是在 CAS 伺服器上發出。

1.  重新啟動Exchange後端伺服器上的 IMAP4 服務。如需停止和啟動 IMAP4 服務的詳細資訊，請參閱[啟動及停止 IMAP4 服務](https://technet.microsoft.com/zh-tw/library/bb124022\(v=exchg.150\))

2.  重新執行關聯的探查，如Verifying the issue still exists一節的步驟 2.c. 所示。

3.  如果問題仍然存在，您必須開啟 IMAP 通訊協定記錄可協助解決問題。若要這樣做，請遵循下列步驟：
    
    1.  在 Windows PowerShell 中執行下列命令：
        
            Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $true
    
    2.  重新啟動Exchange後端伺服器上的 IMAP4 服務。如需如何停止及啟動 IMAP4 服務的詳細資訊，請參閱[啟動及停止 IMAP4 服務](https://technet.microsoft.com/zh-tw/library/bb124022\(v=exchg.150\))
    
    3.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。
    
    4.  執行下列命令，並再決定記錄檔的位置。若要這樣做，執行下列命令：
        
            Get-ImapSettings -server <CAS server name>
    
    5.  決定提供此命令的信箱。信箱伺服器的名稱是在錯誤訊息的`_Mbx:`值的值。
    
    6.  執行下列命令：
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "IMAP*"}
        
        **附註**   在此命令中，請將 *mailbox1.contoso.com* 取代為實際的 Mailbox Server 名稱。
    
    7.  如果任一命令輸出中所列的監視器報告為不健康，必須先解決這些監視器。遵循ImapTestDeepMonitor 和 ImapSelfTestMonitor 復原動作一節所述的疑難排解步驟。

4.  如果 Mailbox Server 回報為狀況良好，請重新啟動 CAS。

5.  重新啟動伺服器之後，重新執行關聯的探查，如Verifying the issue still exists一節的步驟 2c 所示。

6.  關閉通訊協定記錄。若要這樣做，執行下列Windows PowerShell 命令：
    
        Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  重新啟動 IMAP4 服務。

8.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## ImapProxyTestMonitor 復原動作

1.  重新啟動 IMAP4 服務。

2.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

3.  如果探查仍然失敗，請重新啟動 CAS。

4.  重新啟動伺服器之後，重新執行關聯的探查，如Verifying the issue still exists一節的步驟 2c 所示。

5.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## AverageCommandProcessingTimeGt60sMonitor RequestsQueuedGt500Monitor 復原動作

此監視器警示通常是在 CA 和 Mailbox Server 上發出。

1.  重新啟動Exchange上的後端伺服器或 CAS IMAP4 服務。如需如何停止及啟動 IMAP4 服務的詳細資訊，請參閱[啟動及停止 IMAP4 服務](https://technet.microsoft.com/zh-tw/library/bb124022\(v=exchg.150\))

2.  等候 10 分鐘，以查看是否保持狀況良好監視器。在 10 分鐘後執行下列命令：
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    **附註**   在此命令中，請以實際的伺服器名稱取代 *server1.contoso.com*。

3.  等待 10 分鐘，然後重新執行步驟 2 中顯示的命令，查看監視器是否維持健全狀態。

4.  如果問題仍然存在，您必須重新啟動伺服器。CAS 伺服器時，只會重新啟動伺服器。信箱伺服器之伺服器時，請執行下列動作：
    
    1.  容錯移轉伺服器裝載的資料庫。若要這樣做，執行下列命令：
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **附註**   在這個及所有後續程式碼範例中，請以實際的伺服器名稱取代 *server1.contoso.com*。
    
    2.  確認已移動所有資料庫成功關閉回報問題的伺服器。若要這樣做，執行下列命令：
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        如果命令輸出顯示伺服器上沒有主動副本，請重新啟動伺服器。

5.  伺服器重新啟動之後，等待 10 分鐘，然後重新執行步驟 2 中顯示的命令，查看監視器是否仍然狀況良好。

6.  如果監視器維持健全狀態，且這是 Mailbox Server，則執行下列命令來容錯移轉資料庫：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange Server 2013 中的 POP3 和 IMAP4](https://technet.microsoft.com/zh-tw/library/jj657728\(v=exchg.150\))

[啟用 Exchange 2016 的 IMAP4](https://technet.microsoft.com/zh-tw/library/bb124489\(v=exchg.150\))

[Test-ImapConnectivity](https://technet.microsoft.com/zh-tw/library/bb738126\(v=exchg.150\))

