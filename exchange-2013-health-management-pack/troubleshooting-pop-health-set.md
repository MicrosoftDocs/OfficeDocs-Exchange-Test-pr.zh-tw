---
title: 疑難排解 POP 健全設定
TOCTitle: 疑難排解 POP 健全設定
ms:assetid: 6114e9fe-d037-4cb9-a643-933eb5fabc45
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.pop(v=EXCHG.150)
ms:contentKeyID: 53276405
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 POP 健全設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

POP 健全設定監視的整體狀況與可用性的Microsoft Exchange POP3 服務和 POP3 用戶端連線。下列的健全設定密切相關 POP 健全設定：

  - [疑難排解 POP。通訊協定健全設定](troubleshooting-pop-protocol-health-set.md)

  - [疑難排解 POP。Proxy 健全設定](troubleshooting-pop-proxy-health-set.md)

如果您收到警示，指出 POP 服務的狀況不良，表示可能有問題令使用者無法使用在 Exchange 環境中使用 POP3 來存取信箱。

## 說明

POP 服務是透過下列探查與監視器受到監視。


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
<td><p>PopCTPProbe</p></td>
<td><p>POP</p></td>
<td><p>Active Directory</p>
<p>驗證</p>
<p>Mailbox Server 驗證</p>
<p>資訊儲存庫</p>
<p>高可用性</p>
<p>網路</p></td>
<td><p>PopCTPMonitor (POP 健全設定)</p></td>
</tr>
<tr class="even">
<td><p>PopProxyTestProbe</p></td>
<td><p>POP.Proxy</p></td>
<td><p>無</p></td>
<td><p>PopProxyTestMonitor (POP.Proxy 健全設定)</p></td>
</tr>
<tr class="odd">
<td><p>PopDeepTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Active Directory</p>
<p>驗證</p>
<p>資訊儲存庫</p>
<p>高可用性</p></td>
<td><p>PopDeepTestMonitor (POP.Protocol 健全設定)</p></td>
</tr>
<tr class="even">
<td><p>PopSelfTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>無</p></td>
<td><p>PopSelfTestMonitor (POP.Protocol 健全設定)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (POP 健全設定)</p></td>
</tr>
</tbody>
</table>


## 使用者動作

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取 server1.contoso.com 的 POP 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "POP"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  請為不健康狀態監視重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**PopCTPMonitor**。相關聯的監視探查是**PopCTPProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe POP\PopCTPProbe -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## PopTestDeepMonitor 和 PopSelfTestMonitor 復原動作

此監視器警示通常是在 Mailbox Server 上發出。

1.  重新啟動 POP3 後端服務。如需詳細資訊，請參閱[啟動及停止 \[POP3 服務](https://technet.microsoft.com/zh-tw/library/aa997475\(v=exchg.150\))。

2.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

3.  如果探查仍然失敗，請使用下列命令，將 Mailbox Server 上裝載的資料庫容錯移轉：
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  會從信箱伺服器移除所有資料庫之後，您必須先確認已順利移動資料庫。若要這樣做，執行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status

5.  請確定伺服器不主控所有主動副本的資料庫。然後重新啟動伺服器。

6.  成功重新啟動伺服器後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

7.  如果探查成功，請執行下列命令來容錯移轉資料庫：
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

8.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## POPCTPMonitor 復原動作

此監視器警示通常是在 CA 伺服器 (CAS) 上發出。

1.  重新啟動 POP3 服務正在執行的 CAS 角色的伺服器上。如需詳細資訊，請參閱[啟動及停止 \[POP3 服務](https://technet.microsoft.com/zh-tw/library/aa997475\(v=exchg.150\))。

2.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

3.  如果問題仍然存在，請在 Windows PowerShell 中執行下列命令：
    
    1.  ``` 
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $true
        ```
    
    2.  在執行 CAS 角色的伺服器上重新啟動 POP3 服務。
    
    3.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。
    
    4.  執行下列命令，然後找出記錄檔的位置：
        
            Get-PopSettings -server <CAS server name>
    
    5.  執行下列命令，以比較時間戳記和探查來判斷是由哪個信箱來服務該命令：
        
            Get-ServerHealth <mailbox server name> | ?{ $_.HealthSetName -like "POP*"}
    
    6.  如果有任何伺服器回報為狀況不良，請遵循 PopTestDeepMonitor and PopSelfTestMonitor Recovery Actions一節中列出的步驟。

4.  如果 Mailbox Server 回報為狀況良好，請重新啟動 CAS。

5.  伺服器重新啟動後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

6.  執行下列命令來關閉通訊協定記錄功能：
    
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  重新啟動 POP3 服務正在執行的 CAS 角色的伺服器上。如需詳細資訊，請參閱[啟動及停止 \[POP3 服務](https://technet.microsoft.com/zh-tw/library/aa997475\(v=exchg.150\))。

8.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## PopProxyTestMonitor 復原動作

1.  重新啟動 POP3 服務正在執行的 CAS 角色的伺服器上。如需詳細資訊，請參閱[啟動及停止 \[POP3 服務](https://technet.microsoft.com/zh-tw/library/aa997475\(v=exchg.150\))。

2.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

3.  如果探查持續失敗，請重新啟動 CAS。

4.  伺服器重新啟動後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

5.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## AverageCommandProcessingTimeGt60sMonitor 復原動作

此監視器警示通常是在 CA 或 Mailbox Server 上發出。

1.  重新啟動 CA 或信箱伺服器上的 POP3 服務。如需詳細資訊，請參閱[啟動及停止 \[POP3 服務](https://technet.microsoft.com/zh-tw/library/aa997475\(v=exchg.150\))。

2.  等候 10 分鐘，以查看是否保持狀況良好監視器。在 10 分鐘後執行下列命令 （此範例會使用 server1.contoso.com）。
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "POP*"}

3.  如果問題仍然存在，您需要重新啟動伺服器。CAS 伺服器時，只會重新啟動伺服器。如果伺服器是信箱伺服器，必須容錯移轉資料庫，並驗證結果。若要這樣做，請遵循下列步驟：
    
    1.  使用下列命令將伺服器上裝載的資料庫容錯移轉：
        
            Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **附註**   在這個及所有後續程式碼範例中，請將 *server1.contoso.com* 取代為實際的伺服器名稱。
    
    2.  確認已移動所有資料庫成功關閉回報問題的伺服器。若要這樣做，執行下列命令：
        
            Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status
        
        如果命令輸出顯示伺服器上沒有主動副本，請重新啟動伺服器。

4.  伺服器重新啟動之後，等待 10 分鐘，然後重新執行步驟 2 中顯示的命令，查看監視器是否仍然狀況良好。

5.  如果監視器狀況良好，且這是 Mailbox Server，則執行下列命令將資料庫容錯移轉回到 Mailbox Server：
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

6.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[啟動及停止 \[POP3 服務](https://technet.microsoft.com/zh-tw/library/aa997475\(v=exchg.150\))

[Test-PopConnectivity](https://technet.microsoft.com/zh-tw/library/bb738143\(v=exchg.150\))

