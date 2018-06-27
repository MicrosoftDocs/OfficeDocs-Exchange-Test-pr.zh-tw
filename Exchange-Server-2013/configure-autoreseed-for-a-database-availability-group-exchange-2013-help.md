---
title: 'AutoReseed 的設定資料庫可用性群組: Exchange 2013 Help'
TOCTitle: AutoReseed 的設定資料庫可用性群組
ms:assetid: 4a8bd779-b52a-40ed-8040-4d76eabeb41e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619303(v=EXCHG.150)
ms:contentKeyID: 50473183
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AutoReseed 的設定資料庫可用性群組

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-04-15_

AutoReseed 是快速地還原資料庫備援磁碟故障後的功能。如果磁碟失敗，儲存在該磁碟上的資料庫副本會自動重新植入 Mailbox server 上預先設定備用磁碟。您可以使用本主題中的步驟來設定 AutoReseed 的資料庫可用性群組 (DAG)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>AutoReseed 功能不會讓您執行任何必要的設定工作。新增至系統的備用磁碟、 更換故障磁碟及格式設定新的磁碟正確，安裝磁碟必須以手動方式來完成系統管理員。</td>
</tr>
</tbody>
</table>


如需與 DAG 相關的其他管理工作，請參閱[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成這項工作預估時間： 10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md) 主題中的「資料庫可用性群組」項目。

  - 必須為每個實體磁碟建立一個邏輯磁碟/磁碟分割。

  - 必須使用以下步驟描述的特定資料庫和記錄檔資料夾結構。

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


## 該怎麼做？

## 步驟 1： 設定資料庫和磁碟區根路徑

第一個步驟包括設定資料庫 (*AutoDagDatabasesRootFolderPath*) 和磁碟區 (*AutoDagVolumesRootFolderPath*) 由 DAG 的根目錄。預設值且 C:\\ExchangeDatabases，C:\\ExchangeVolumes，分別。您可以省略此步驟如果您使用預設的路徑。

此範例說明如何設定資料庫的根路徑。

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabasesRootFolderPath "C:\ExchDbs"

此範例說明如何設定儲存磁碟區的根路徑。

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagVolumesRootFolderPath "C:\ExchVols"

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功設定資料庫與磁碟區的根路徑，請執行以下命令。

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

*AutoDagDatabasesRootFolderPath* 與 *AutoDagVolumesRootFolderPath* 的輸入應該反映設定的路徑。

## 步驟 2： 設定每個磁碟區的資料庫數目

接著，為 DAG 設定每個磁碟區 (*AutoDagDatabaseCopiesPerVolume*) 的資料庫數量。

此範例說明如何為已設為每一個磁碟區有 4 個資料庫的 DAG 設定此 AutoReseed 設定。

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabaseCopiesPerVolume 4

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功設定每一個磁碟區的資料庫數量，請執行以下命令。

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

*AutoDagDatabaseCopiesPerVolume* 的輸出應該反映設定值。

## 步驟 3： 建立資料庫與磁碟區的根目錄

接著，建立您在步驟 1 中所設定之根目錄所對應的目錄。此範例顯示如何使用命令提示字元建立預設目錄。

    md C:\ExchangeDatabases
    md C:\ExchangeVolumes

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功設定資料庫與磁碟區的根目錄，請執行以下命令。

    Dir C:\

建立的目錄應出現在輸出清單中。

## 步驟 4： 裝載大量資料夾

為要用於資料庫 （包括備用磁碟區） 的每個磁碟區使用的 Windows 磁碟管理應用程式 (diskmgmt.msc) 來裝載下 C:\\ExchangeVolumes\\ 裝載資料夾中的每個磁碟區。例如，如果有 2 的磁碟區與資料庫和 1 備用磁碟區，裝載至下列裝載資料夾的磁碟區：

  - C:\\ExchangeVolumes\\Volume1

  - C:\\ExchangeVolumes\\Volume2

  - C:\\ExchangeVolumes\\Volume3

只要將資料夾裝載在根磁碟區的路徑下，裝載的資料夾名稱便可以是任何資料夾名稱。

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功裝載磁碟區資料夾，請執行以下命令。

    Dir C:\

裝載的磁碟區應該出現在輸出清單中。

## 步驟 5： 建立的資料庫資料夾

接下來，建立根路徑 C:\\ExchangeDatabases 下的 \[資料庫\] 目錄。本範例會說明如何使用 4 個資料庫在每個磁碟區上建立目錄的儲存設定。

    md c:\ExchangeDatabases\db001

    md c:\ExchangeDatabases\db002

    md c:\ExchangeDatabases\db003

    md c:\ExchangeDatabases\db004

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功裝載資料庫資料夾，請執行以下命令。

    Dir C:\ExchangeDatabases

建立的目錄應出現在輸出清單中。

## 步驟 6： 建立資料庫的掛接點

建立每個資料庫的掛接點並連結到正確的磁碟區掛接點。例如，db001 裝載的資料夾應該在 C:\\ExchangeDatabases\\db001。您可以使用 diskmgmt.msc 或 mountvol.exe 為達成此目的。本範例會說明如何裝載至 C:\\ExchangeDatabases\\db001 使用 mountvol.exe db001。

    Mountvol.exe c:\ExchangeDatabases\db001 \\?\Volume (GUID)

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功建立資料庫的掛接點，請執行以下命令。

    Mountvol.exe C:\ExchangeDatabases\db001 /L

裝載的磁碟區應該出現在掛接點清單中。

## 步驟 7： 建立資料庫的目錄結構

接下來，建立兩個目錄移至 \[您在步驟 5 中，一個適用於每個資料庫，其中每個資料庫的記錄資料流會儲存在相同的磁碟區中建立的資料夾。您必須使用下列格式的目錄結構：

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.db

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.log

此範例說明如何為儲存在磁碟區 1 的 4 個資料庫建立目錄：

    md c:\ExchangeDatabases\db001\db001.db

    md c:\ExchangeDatabases\db001\db001.log

    md c:\ExchangeDatabases\db002\db002.db

    md c:\ExchangeDatabases\db002\db002.log

    md c:\ExchangeDatabases\db003\db003.db

    md c:\ExchangeDatabases\db003\db003.log

    md c:\ExchangeDatabases\db004\db004.db

    md c:\ExchangeDatabases\db004\db004.log

對每一個磁碟區上的資料庫重複以上命令。

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功建立資料庫目錄架構，請執行以下命令。

    Dir C:\ExchangeDatabases /s

建立的目錄應出現在輸出清單中。

## 步驟 8： 建立資料庫

建立資料庫與記錄檔及資料庫設定的適當資料夾的路徑。本範例會說明如何建立儲存新建立的目錄和掛接點結構中的資料庫。

    New-MailboxDatabase -Name db001 -Server MBX1 -LogFolderPath C:\ExchangeDatabases\db001\db001.log -EdbFilePath C:\ExchangeDatabases\db001\db001.db\db001.edb

## 如何才能了解此步驟是否正常運作？

若要確認您已在適當資料夾中成功建立資料庫，請執行以下命令。

    Get-MailboxDatabase db001 | Format List *path*

傳回的資料庫屬性應指明資料庫檔案與記錄檔儲存在上述資料夾中。

## 如何才能了解此工作是否正常運作？

若要確認您已設定 DAG 的 AutoReseed，請執行以下動作：

1.  執行下列命令，確認已正確設定 DAG。
    
        Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

2.  執行下列命令，確認已正確設定目錄架構 (以下為預設路徑；請視需要將路徑替換成您正在使用的路徑)。
    
        Dir c:\ExchangeDatabases /s
    
        Dir c:\ExchangeVolumes /s

