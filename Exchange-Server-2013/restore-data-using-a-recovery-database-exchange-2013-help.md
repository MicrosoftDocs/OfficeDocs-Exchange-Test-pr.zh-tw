---
title: '使用復原資料庫還原資料: Exchange 2013 Help'
TOCTitle: 使用復原資料庫還原資料
ms:assetid: d64c18e7-16af-4bd8-a5c5-01206984d4d1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee332351(v=EXCHG.150)
ms:contentKeyID: 50474348
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用復原資料庫還原資料

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-10-01_

復原資料庫 (RDB) 是特殊種類的信箱資料庫，可讓您在復原作業中從還原的信箱資料庫中裝載和擷取資料。RDB 可讓您從資料庫的備份或副本中復原資料，而不會干擾使用者存取目前的資料。

在建立 RDB 之後，您可以使用備份應用程式或將資料庫及其記錄檔複製到 RDB 資料夾結構中，以此將信箱資料庫還原至 RDB 中。然後您可以使用 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829875\(v=exchg.150\)) 指令程式，從還原的資料庫擷取資料。擷取資料之後，您可以將資料匯出到資料夾或合併到現有信箱中。

如需其他 RDB 相關的管理工作資訊，請參閱 [復原資料庫](recovery-databases-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：1 分鐘，加上使資料庫進入正常關機狀態並擷取資料的時間。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱復原」項目。

  - 有些備份應用程式可以直接將 Exchange 資料還原到復原資料庫。Windows Server Backup 只能將檔案層級備份還原到復原資料庫。它不能用來將應用程式層級的備份還原到復原資料庫。

  - 包含復原之資料的資料庫和記錄檔必須還原或複製到 RDB 資料夾結構中。

  - 資料庫必須是處於正常關閉的狀態。由於 RDB 是所有資料庫的替代還原位置，因此所有還原的資料庫會處於不正常關閉的狀態。您必須使用 **Eseutil /R** 讓還原的資料庫進入正常關閉狀態。

## 使用命令介面，利用復原資料庫來復原資料

1.  將復原的資料庫及其記錄檔複製到 (或將資料庫及其記錄檔還原到) 您要用於復原資料庫的位置。

2.  使用 Eseutil 讓該資料庫進入正常關閉狀態。在下列範例中，EXX 是資料庫的記錄檔產生前置詞 (例如，E00，E01，E02，以此類推)。
    
        Eseutil /R EXX /l <RDBLogFilePath> /d <RDBEdbFolder>
    
    下列範例說明記錄檔產生前置詞 E01 及復原資料庫和記錄檔路徑 E:\\Databases\\RDB1：
    
        Eseutil /R E01 /l E:\Databases\RDB1 /d E:\Databases\RDB1

3.  建立復原資料庫。指定唯一名稱給復原資料庫，但在 EdbFilePath 參數中使用資料庫檔案的名稱和路徑，在 LogFolderPath 參數中使用復原的記錄檔的位置。
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath <RDBPathandFileName> -LogFolderPath <LogFilePath>
    
    下列範例說明建立用來復原 DB1.edb 及其記錄檔的復原資料庫，這些都位於 E:\\Databases\\RDB1。
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath "E:\Databases\RDB1\DB1.EDB" -LogFolderPath "E:\Databases\RDB1"

4.  重新啟動 Microsoft Exchange Information Store 服務：
    
        Restart-Service MSExchangeIS

5.  裝載復原資料庫：
    
        Mount-database <RDBName>

6.  請確認已裝載的資料庫中包含您想要還原的信箱：
    
        Get-MailboxStatistics -Database <RDBName> | ft -auto

7.  使用 New-MailboxRestoreRequest 指令程式將信箱或項目從復原資料庫還原至實際執行信箱。
    
    下列範例會將還原的來源信箱的 MailboxGUID 為 1d20855f-fd54-4681-98e6-e249f7326ddd 的別名 Morris 的目標信箱的信箱資料庫 DB1 上。
    
        New-MailboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox 1d20855f-fd54-4681-98e6-e249f7326ddd -TargetMailbox Morris
    
    下列範例會還原到封存信箱的信箱資料庫 DB1 上的顯示名稱 Morris Cornejo 具有 Morris@contoso.com 的來源信箱的內容。
    
        New-MaiboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox "Morris Cornejo" -TargetMailbox Morris@contoso.com -TargetIsArchive

8.  使用 [Get-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829907\(v=exchg.150\)) 定期檢查信箱還原要求的狀態。
    
    當還原的狀態為「已完成」時，使用 [Remove-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829910\(v=exchg.150\)) 來移除還原要求。例如：
    
        Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest

## 如何才能了解這是否正常運作？

若要確認您是否成功復原信箱資料，請使用 Outlook 或 Outlook Web App 開啟目標信箱，並確認復原的資料是否存在。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>

