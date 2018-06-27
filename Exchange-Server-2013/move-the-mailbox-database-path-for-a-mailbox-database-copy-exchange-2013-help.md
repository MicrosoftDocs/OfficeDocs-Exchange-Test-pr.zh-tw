---
title: '移動信箱資料庫複本的信箱資料庫路徑: Exchange 2013 Help'
TOCTitle: 移動信箱資料庫複本的信箱資料庫路徑
ms:assetid: 324f255c-d95d-4a8a-a134-c8cee5c5b9cb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd979782(v=EXCHG.150)
ms:contentKeyID: 50472811
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移動信箱資料庫複本的信箱資料庫路徑

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-05-07_

建立信箱資料庫之後，您可以使用 EAC 或命令介面，將其移至另一個磁碟區、資料夾、位置或路徑。如需如何移動非覆寫信箱資料庫之信箱資料庫路徑的逐步指示，請參閱[Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。

如果要移動的信箱資料庫複寫到一個或多個信箱資料庫副本，您必須遵循本主題中的程序移動信箱資料庫路徑。信箱資料庫的所有副本都必須位於主控副本的每個伺服器上的相同路徑中。例如，如果資料庫 DB1 在伺服器 EX1 上位於 C:\\mountpoints\\DB1，則在伺服器 EX2、EX3 等等上的 DB1 的副本也必須位於 C:\\mountpoints\\DB1。

要尋找與信箱資料庫副本相關的其他管理工作嗎？請參閱[管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：2 分鐘，加上移動資料的時間 (視各種因素而定) ，例如資料庫大小、速度、可用頻寬與網路延遲以及儲存裝置速度。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主題中的「信箱資料庫副本」項目。

  - 若要執行移動作業，資料庫必須暫時卸載，使所有使用者無法存取。若資料庫目前已卸載，則完成後不會重新裝載。

  - 若要執行移動作業，資料庫的所有副本必須停用複寫。暫停複寫還不足夠，您必須使用 [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335119\(v=exchg.150\)) 指令程式移除資料庫副本以便將其停用。

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


## 使用命令介面將複寫信箱資料庫移至新路徑

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 將複寫信箱資料庫移至新路徑。</td>
</tr>
</tbody>
</table>


1.  請注意，信箱資料庫所有副本的重新執行延遲或截斷延遲設定都將移動。您可以使用 [Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\)) 指令程式取得此資訊，如此範例中所示。
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  如果爲資料庫啟用循環記錄，則在繼續之前必須將其停用。您可以使用 [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\)) 指令程式來停用信箱資料庫的循環記錄，如此範例中所示。
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

3.  移除要移動之資料庫的所有信箱資料庫副本。如需詳細步驟，請參閱[移除信箱資料庫副本](remove-a-mailbox-database-copy-exchange-2013-help.md)。移除所有副本之後，將要移除資料庫副本之每個伺服器的資料庫及交易記錄檔移至其他位置來保留這些檔案。這些檔案將保留，因此在重新新增資料庫副本後不需重新植入這些檔案。

4.  將信箱資料庫路徑移至新位置。如需詳細步驟，請參閱[Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>移動作業期間，必須卸載要移動的資料庫。移動完成之前，此處理程序將造成服務中斷，並造成所有使用者與要移除之資料庫上的信箱中斷。移動作業完成後，會自動裝載資料庫。</td>
    </tr>
    </tbody>
    </table>


5.  在先前包含已移除之信箱資料庫被動副本的每個信箱伺服器上，建立所需的資料夾結構。例如，如果您將資料庫移至 C:\\mountpoints\\DB1，則必須在每個信箱伺服器上建立將主控信箱資料庫副本的這個相同路徑。

6.  建立資料夾結構之後，將信箱資料庫及其記錄檔資料流的被動副本移至新位置。這些是在步驟 3 之後留下及保留的檔案。針對在步驟 3 中移除的每個資料庫副本重複此處理程序。

7.  新增在步驟 3 中移除的所有資料庫副本。如需詳細步驟，請參閱[新增信箱資料庫副本](add-a-mailbox-database-copy-exchange-2013-help.md)。

8.  在包含要移動之信箱資料庫副本的每部伺服器上執行下列命令，來停止並重新啟動內容索引服務。
    
        Net stop MSExchangeFastSearch
        Net start MSExchangeFastSearch

9.  或者，使用 [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\)) 指令程式來啟用循環記錄，如此範例中所示。
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

10. 使用 [Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298104\(v=exchg.150\)) 指令程式重新設定任何先前為重新執行延遲時間和截斷延遲時間設定的值。
    
        Set-MailboxDatabaseCopy DB1\MBX2 -ReplayLagTime 00:15:00

11. 新增每個副本時，建議您在新增下一個副本之前，先驗證副本的健康狀況和狀態。您可以使用下列方法驗證健康狀況與狀態：
    
    1.  檢查事件記錄檔中，與資料庫或資料庫副本相關的任何錯誤或警告事件。
    
    2.  使用 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-tw/library/dd298044\(v=exchg.150\)) 指令程式檢查資料庫副本連續複寫的健康狀況和狀態。
    
    3.  使用 [Test-ReplicationHealth](https://technet.microsoft.com/zh-tw/library/bb691314\(v=exchg.150\)) 指令程式驗證資料庫可用性群組和連續複寫的健康狀況和狀態。

如需詳細的語法及參數資訊，請參閱下列主題：

  - [Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\))

  - [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\))

  - [Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298104\(v=exchg.150\))

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-tw/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/zh-tw/library/bb691314\(v=exchg.150\))

## 如何知道這是否正常運作？

若要驗證是否成功移動信箱資料庫副本的路徑，請執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[伺服器\] \> \[資料庫\]。  選擇已付置的資料庫。在 \[詳細資料\] 窗格中，將顯示資料庫複本的狀態與其內容索引，以及目前的複本佇列長度。確認其狀態為 \[正常\]。

  - 在命令介面中，執行下列指令以確認已建立信箱資料庫副本與其狀況：
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    狀態與內容索引狀態皆應為 \[正常\]。

