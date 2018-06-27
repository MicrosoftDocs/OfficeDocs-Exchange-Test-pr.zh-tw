---
title: '更新信箱資料庫副本: Exchange 2013 Help'
TOCTitle: 更新信箱資料庫副本
ms:assetid: bead3cc5-7d50-446f-95b7-e432bcb7968e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351100(v=EXCHG.150)
ms:contentKeyID: 50474145
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更新信箱資料庫副本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-02_

更新，也稱為*植入*，是信箱資料庫複本新增至資料庫可用性群組 (DAG) 中的其他 Mailbox server 中的程序。新加入的複本成為被動副本重新顯示記錄檔從作用中副本複製所放入其中的比較基準資料庫。在下列情況下所需植入：

  - 建立新的被動資料庫複本時。可以延遲植入新的信箱資料庫副本，但最後每個被動資料庫副本必須植入運作作為備援的資料庫副本。

  - 容錯移轉會發生在哪些資料之後會遺失因為具有成為發散且無法復原被動資料庫副本。

  - 當系統偵測到損毀的記錄檔，無法將資料庫的被動副本重新顯示。

  - 在任何資料庫副本的離線磁碟重組之後發生。

  - 記錄之後產生順序資料庫具有已重設回 1。

您可以執行植入使用下列方法：

  - **自動植入**  自動植入產生的目標信箱伺服器上的作用中資料庫的被動副本。自動植入會發生在建立的資料庫。

  - **植入使用 Update-mailboxdatabasecopy 指令程式**  您可以使用命令介面中的[Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\))指令程式來植入資料庫副本任何時候。

  - **植入使用更新的信箱資料庫副本精靈**  您可以使用 EAC 中更新信箱資料庫副本精靈來隨時植入資料庫副本。

  - **手動複製離線的資料庫**  您可以卸載資料庫的主動副本並將資料庫檔案複製到相同 DAG 中的另一個信箱伺服器上的相同位置。如果您使用此方法，將會中斷服務中的因為程序需要您卸載資料庫。

更新的資料庫副本可能需要很長的時間，尤其是當要複製的資料庫是大型或高網路延遲或低網路頻寬。在啟動植入程序之後，不要關閉 EAC 或命令介面直到完成程序。如果您這樣做，會終止植入操作。

資料庫副本可以為來源使用作用中副本或最新的被動副本植入植入。當從被動副本植入，注意植入作業會終止在下列情況下網路通訊錯誤：

  - 如果狀態植入來源複製失敗或變更 FailedAndSuspended。

  - 如果資料庫容錯移轉至另一個副本。

多個資料庫副本可以同時植入。不過，當同時植入多個複本，必須植入僅資料庫檔案，並省略內容索引類別目錄。您可以使用*DatabaseOnly*參數與[Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\))指令程式來這麼做。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您未使用<em>DatabaseOnly</em>參數植入多部目標從相同的來源時，工作會與 SeedInProgressException 錯誤 FE1C6491 失敗。</td>
</tr>
</tbody>
</table>


要尋找與信箱資料庫副本相關的其他管理工作嗎？請參閱[管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成這項工作預估時間： 2 分鐘，加上的時間來植入資料庫副本，這取決於在各種因素，如資料庫、 速度、 可用頻寬和延遲的網路、 大小和儲存速度。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主題中的「信箱資料庫副本」項目。

  - 必須擱置信箱資料庫副本。如需詳細步驟，請參閱[擱置或恢復信箱資料庫副本](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md)。

  - 必須裝載您正在更新被動資料庫副本的伺服器上執行遠端登錄服務。

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

## 使用 EAC 來更新信箱資料庫副本

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  選取您要更新的被動副本的信箱資料庫。

3.  在 \[詳細資料\] 窗格中的 \[**資料庫副本**，按一下 \[**擱置**下您想要植入被動資料庫副本。提供任何選擇性的註解，並按一下 \[**儲存**\]。

4.  在 \[詳細資料\] 窗格中的 \[**資料庫副本**，按一下 \[**更新**下您想要植入被動資料庫副本。

5.  
    
    根據預設，使用中資料庫副本的來源資料庫植入時才使用。如果您偏好使用之資料庫的被動副本植入，請按一下 \[選取包含您想要使用的來源被動資料庫副本的伺服器的 \[**瀏覽...** \]。

6.  按一下 \[**儲存**\] 以更新被動資料庫副本。

## 使用命令介面來更新信箱資料庫副本

本範例會示範如何植入 MBX1 上資料庫 DB1 的複本。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1

本範例會示範如何植入資料庫 DB1 的副本 MBX1 上使用植入來源信箱伺服器 MBX2。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2

本範例會示範如何不含植入內容索引類別目錄植入 MBX1 上資料庫 DB1 的複本。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -DatabaseOnly

本範例會示範如何植入內容索引類別目錄 MBX1 上資料庫 DB1 副本沒有植入資料庫檔案。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

## 手動複製離線的資料庫

1.  如果爲資料庫啟用循環記錄，則在繼續之前必須將其停用。您可以使用 [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\)) 指令程式來停用信箱資料庫的循環記錄，如此範例中所示。
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

2.  卸載資料庫。您可以使用[Dismount-Database](https://technet.microsoft.com/zh-tw/library/bb124936\(v=exchg.150\))指令程式，此範例所示。
    
        Dismount-Database DB1 -Confirm $false

3.  手動將資料庫檔案 （資料庫檔案與所有記錄檔） 複製到第二個位置，例如外部的磁碟機或網路共用。

4.  裝載的資料庫。您可以使用[Mount-Database](https://technet.microsoft.com/zh-tw/library/aa998871\(v=exchg.150\))指令程式，此範例所示。
    
        Mount-Database DB1

5.  在伺服器上主控之複本，複製資料庫檔案的外部的磁碟機或網路共用相同路徑為作用中資料庫副本。例如，如果作用中副本的資料庫路徑是 D:\\DB1\\DB1.edb 及記錄檔路徑是 D:\\DB1，您將資料庫將檔案複製到 D:\\DB1 主控之複本的伺服器上。

6.  此範例所示使用*SeedingPostponed*參數使用[Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298105\(v=exchg.150\))指令程式新增信箱資料庫副本。
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -SeedingPostponed

7.  如果資料庫啟用循環記錄，啟用它再次使用[Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\))指令程式，此範例所示。
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

## 如何知道這是否正常運作？

若要驗證您是否已成功植入信箱資料庫複本，請執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[**伺服器**\>**資料庫**。選取已植入資料庫。在 \[詳細資料\] 窗格中會顯示的資料庫副本和其內容索引狀態，以及目前的複製佇列長度。

  - 在命令介面中執行下列命令來確認信箱資料庫副本成功植入且狀況良好。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    狀態與內容索引狀態皆應為 \[正常\]。

