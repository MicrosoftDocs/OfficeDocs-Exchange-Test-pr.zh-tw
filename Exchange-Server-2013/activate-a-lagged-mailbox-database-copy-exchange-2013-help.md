---
title: '啟動延遲的信箱資料庫副本: Exchange 2013 Help'
TOCTitle: 啟動延遲的信箱資料庫副本
ms:assetid: 493d9c40-644d-49d6-9291-949acbcfdcb6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd979786(v=EXCHG.150)
ms:contentKeyID: 50473064
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟動延遲的信箱資料庫副本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-01-28_

延遲的信箱資料庫副本是重新顯示延遲時間值設定為大於 0 的信箱資料庫副本。如果您要資料庫重新顯示所有記錄檔，並且讓資料庫副本保持最新狀態，啟動和復原延遲的信箱資料庫副本會是相當簡單的程序。如果您要重新顯示截至某一個特定時間點記錄檔，這會是較困難的作業，因爲您必須手動操作記錄檔並執行 Eseutil。

要尋找其他與延遲的信箱資料庫副本有關的資訊嗎？請參閱[管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>啟動延遲的信箱資料庫副本所需的時間，直接取决於需要重新顯示的記錄檔數量，以及硬體重新顯示這些檔案的速度。不過，您的每個資料庫每秒應至少可重新顯示兩個記錄。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 完成此工作的預估時間：1 分鐘，加上複製延遲副本、重新顯示必要的記錄檔以及擷取資料或資料庫以供用戶端活動使用的時間。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主題中的「信箱資料庫副本」項目。

  - 啟動的信箱資料庫副本的重新顯示延遲時間設定必須大於 0。

  - 啟動的信箱資料庫副本必須擁有要復原的時間點之前的所有記錄檔。務必記得，判斷要復原的時間點時，資料庫交易可能跨越多個記錄檔。

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


## 您要執行的工作

## 使用命令介面將延遲的信箱資料庫副本啟動至特定時間點

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 將延遲的信箱資料庫副本啟動至特定時間點。不過，您可以使用命令介面與指令命令列執行一系列步驟。</td>
</tr>
</tbody>
</table>


1.  此範例會使用 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd351074\(v=exchg.150\)) 指令程式暫停正在啟動之延遲副本的複寫。
    
        Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false

2.  選擇性地 (為保存延遲副本) 製作資料庫副本和記錄檔的副本。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此時，繼續在現有磁碟區上執行此程序，會在寫入效能大幅下降的情況下產生副本。如果不希望發生這種情況，您可以將資料庫和記錄檔複製到另一個磁碟區進行復原。</td>
    </tr>
    </tbody>
    </table>


3.  決定需要將哪些記錄檔重新顯示到資料庫中，以符合此復原作業的時間點需求 (根據記錄檔日期和時間，如 Windows 檔案總管中所示)。在此時間點之後建立的所有記錄檔都應移至不同的目錄，直到復原程序完成且不再需要記錄檔為止。

4.  刪除資料庫的檢查點 (.chk) 檔案。

5.  此範例會使用 Eseutil 執行復原作業。
    
        Eseutil.exe /r eXX /a
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在上面的範例中，e<em>XX</em> 是資料庫的記錄檔產生前置詞 (例如，E00，E01，E02，以此類推)。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此步驟可能需要相當長的時間，取决於幾個因素，例如重新顯示延遲時間的長度、這段時間內產生的記錄檔的數目，以及硬碟將這些記錄檔重新顯示到要復原的資料庫中的速度。</td>
    </tr>
    </tbody>
    </table>


6.  記錄檔重新顯示完成之後，資料庫會處於正常關機狀態，並且可以複製和用於復原。

7.  復原程序完成後，此範例會繼續進行復原程序中使用的資料庫複寫作業。
    
        Resume-MailboxDatabaseCopy DB1\EX3

如需詳細的語法及參數資訊，請參閱 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd351074\(v=exchg.150\)) 或 [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335220\(v=exchg.150\))。

## 使用命令介面，透過重複顯示所有未認可的日誌檔案來啟動延遲信箱資料庫

1.  選擇性地 (為保存延遲副本) 製作資料庫副本和記錄檔的副本。
    
    1.  此範例會使用 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd351074\(v=exchg.150\)) 指令程式暫停正在啟動之延遲副本的複寫。
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  選擇性地 (為保存延遲副本) 製作資料庫副本和記錄檔的副本。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>此時，繼續在現有磁碟區上執行此程序，會在寫入效能大幅下降的情況下產生副本。如果不希望發生這種情況，您可以將資料庫和記錄檔複製到另一個磁碟區進行復原。</td>
        </tr>
        </tbody>
        </table>


2.  此範例會使用 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-tw/library/dd298068\(v=exchg.150\)) 指令程式搭配 *SkipLagChecks* 參數，啟動延遲信箱資料庫副本。
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -SkipLagChecks

## 在命令介面中使用 SafetyNet 復原啟動延遲信箱資料庫副本

1.  或者（為保存遲延複本），拍攝包含資料庫副本及其記錄檔之磁碟區的檔案系統 (非 Exchange 感知) 磁碟區陰影複製服務 (VSS) 快照。
    
    1.  此範例會使用 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd351074\(v=exchg.150\)) 指令程式暫停正在啟動之延遲副本的複寫。
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  選擇性地 (為保存延遲副本) 製作資料庫副本和記錄檔的副本。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>此時，繼續在現有磁碟區上執行此程序會引發寫入時複製效能減損。如果不希望發生這種情況，您可以將資料庫和記錄檔複製到另一個磁碟區進行復原。</td>
        </tr>
        </tbody>
        </table>


2.  尋找 ESEUTIL 資料庫標頭輸出中的 "Log Required:" 值，藉此判斷延遲資料庫副本所需的記錄數
    
        Eseutil /mh <DBPath> | findstr /c:"Log Required"
    
    記下括號內的十六進位數值。第一個數值是所需的最低層代 (稱為 LowGeneration)，第二個數值是所需的最高層代 (稱為 HighGeneration)。將所有層代序號大於 HighGeneration 的記錄檔層代檔案移動到不同的位置，使其無法在資料庫中重新顯示。

3.  在主控資料庫主動副本的伺服器上，刪除從主動副本啟動之延遲副本的記錄檔，或停止 Microsoft Exchange 複寫服務。

4.  執行資料庫轉換並啟動延遲副本。此範例會使用 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-tw/library/dd298068\(v=exchg.150\)) 指令程式搭配數個參數來啟動資料庫。
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -MountDialOverride BestEffort -SkipActiveCopyChecks -SkipClientExperienceChecks -SkipHealthChecks -SkipLagChecks

5.  這時資料庫將自動裝載並要求 SafetyNet 重新傳遞遺失的郵件。

## 如何知道這是否正常運作？

若要確認您是否已成功啟動延遲信箱資料庫副本，請進行下列其中一項：

  - 在 EAC 中，瀏覽至 \[伺服器\] \> \[資料庫\]。  選擇適當的資料庫，並在 \[詳細資料\] 窗格中檢視資料庫複本屬性。

  - 在命令介面中，執行下列指令以顯示資料庫副本的狀態資訊。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

