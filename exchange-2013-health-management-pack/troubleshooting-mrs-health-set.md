---
title: 疑難排解 MRS 健全設定
TOCTitle: 疑難排解 MRS 健全設定
ms:assetid: 21947ed6-1584-4db9-9cd6-f6c1de22e352
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.mrs(v=EXCHG.150)
ms:contentKeyID: 53276398
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 MRS 健全設定

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2015-03-09_

信箱複寫服務 (MRS) 健全設定會監視 MRS 服務的整體健全狀況。

## 說明

MRS 服務的監視可以使用下列探查和監視器。


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
<td><p>MRSServiceCrashingProbe</p></td>
<td><p>MRS</p></td>
<td><p>資訊儲存庫</p></td>
<td><p>MRSServiceCrashingMonitor</p></td>
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
        
        例如，若要擷取關於 server1.contoso.com 的 MRS 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "MRS"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  處於不健全的狀態監視器，重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視器是**MRSServiceCrashingMonitor**。與該監視器有關的探查是**MRSServiceCrashingProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe MRS\MRSServiceCrashingProbe -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## 常見問題

當您收到健全設定的警示時，電子郵件訊息會包含下列資訊：

  - 傳送警示的伺服器名稱

  - 警示的發生日期和時間

  - 所使用的驗證機制及認證資訊

  - 上一個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊
    
    您可以使用完整的例外狀況追蹤中的資訊，以協助疑難排解問題。探查所產生的例外狀況包含描述探查失敗的原因失敗原因。

**信箱鎖定**

信箱鎖定時，您可能會收到類似如下的警示：

*MailboxIdentity: namprd03.prod.outlook.com/Microsoft Exchange Hosted Organizations/example.com/User6 MailboxGuid: Primary (00000000-abcd-01234-5678-1234567890ab) RequestFlags: IntraOrg, Pull, Protected Database: exampledb-db089 Exception: MapiExceptionADUnavailable: Unable to prepopulate the cache for user …*

這表示信箱已被鎖定。若要解除鎖定信箱，請執行下列命令 ︰

    New-MailboxRepairRequest -CorruptionType LockedMoveTarget -Identity <mailboxIdentity> [-Archive]

**附註**  這個命令中，請將 \<*mailboxIdentity*\> 取代為**MailboxIdentity**的電子郵件訊息中所提供的信箱名稱。如果信箱已封存信箱，則必須包含**– 封存**旗標。您可以判斷信箱是否為主要或封存信箱，藉由檢視警示中的 \[ **MailboxGuid** \] 欄位。

**損毀移轉工作**

發生損毀的移轉工作時，您可能會收到類似如下的警示：

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Details: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

當移轉中繼資料發生問題時，就會發生損毀。在損毀，Microsoft 會收到將調查 Watson 報告。要修復這個問題，必須移除移轉的批次，然後再重新建立批次。若要這樣做，請遵循下列步驟：

1.  若要移除損毀的批次，請執行下列命令：
    
        Remove-MigrationBatch -Identity

2.  若要重新建立批次工作，請執行下列命令：
    
        New-MigrationBatch -Local -Name

如需相關資訊，請參閱[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

**警示 MailboxMigration: CriticalError**

在郵件移轉期間發生嚴重錯誤時，您可能會收到類似如下的警示：

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Details: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

若要解決這個問題，您必須重試移轉。若要這樣做，請執行下列命令，或按 \[**開始**\] 按鈕上的 \[Exchange 系統管理中心 (EAC)。

    Call start-migrationbatch -Identity batchName

發生此問題時，Dr. Watson 訊息會傳送至 Microsoft 以進行調查。

**Migration Exchange 複寫服務未執行**

當您看見此錯誤原因時，可以執行下列命令來驗證服務的健全狀態：

    Test-MRSHealth <servername> -MonitoringContext:$true

也可以執行下列命令來嘗試啟動服務：

    Start-Service msexchangemailboxreplication

**MSExchangeMailboxReplication RCP Ping 失敗**

當您看見此錯誤原因時，您可能會收到類似如下的警示：

*An issue with MRS was detected at 6/26/2012 6:08:47 AM. Details: MRS RPC Ping check for server \<ServerName\> failed with the following error: The RPC endpoint for the Microsoft Exchange Mailbox Replication service couldn't respond:*

發生此問題時，可以執行下列命令來驗證服務的健全狀態：

    Test-MRSHealth <servername> -MonitoringContext:$true

也可以執行下列命令來嘗試重新啟動服務：

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication 服務重複損毀**

當 MSExchangeMailboxReplication 服務損毀或停止回應，您可能會收到類似如下的警示：

*The MRS process has crashed at least 3 times in last 01:00:00. \<b\>Watson Message:\</b\> Watson report about to be sent for process id: 41432, with parameters: E12, \<ServerName\>, 15.00.0516.024, MSExchangeMailboxReplication, M.Exchange.MailboxReplicationService, M.E.M.BaseJob.BeginJob, System.ApplicationException, 7ec9, 15.00.0516.024. ErrorReportingEnabled: True.*

發生此問題時，可以執行下列命令來驗證服務的健全狀態：

    Test-MRSHealth <servername> -MonitoringContext:$true

也可以執行下列命令來嘗試重新啟動服務：

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication 未掃描 MDB 佇列**

當 MSExchangeMailboxReplication 服務無法掃描佇列時，您可能會收到類似如下的警示：

*An issue with MRS was detected at 6/12/2012 6:20:44 PM. Details: MRS queue scan check for server \<servername\> failed with the following error: The Microsoft Exchange Mailbox Replication Service isn't scanning mailbox database queues for jobs. Last scan age: 04:38:02.1959439..*

發生此問題時，可以執行下列命令來驗證服務的健全狀態：

    Test-MRSHealth <servername> -MonitoringContext:$true

也可以執行下列命令來嘗試重新啟動服務：

    Restart-Service msexchangemailboxreplication

**其他疑難排解步驟**

1.  啟動 IIS 管理員，然後連線到報告問題的伺服器，驗證 **MSExchangeServicesAppPool** 應用程式集區正在執行中。

2.  在 IIS 管理員中，按一下 **\[應用程式集區\]**，然後從命令介面執行下列命令，回收 **MSExchangeServicesAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  重新執行關聯的探查，如Verifying the issue still exists一節的步驟 2c 所示。

4.  如果問題仍然存在，請使用 IISReset 公用程式回收 IIS 服務，或執行下列命令：
    
        Iisreset /noforce

5.  重新執行關聯的探查，如Verifying the issue still exists一節的步驟 2c 所示。

6.  如果問題仍然存在，請重新啟動伺服器。

7.  重新啟動伺服器之後，重新執行關聯的探查，如Verifying the issue still exists一節的步驟 2c 所示。

8.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

