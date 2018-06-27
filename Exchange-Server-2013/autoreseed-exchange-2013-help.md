---
title: 'AutoReseed: Exchange 2013 Help'
TOCTitle: AutoReseed
ms:assetid: 61f9a8be-070e-4c62-b505-52644fcff0c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn789209(v=EXCHG.150)
ms:contentKeyID: 62523855
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AutoReseed

 

_**適用版本：**Exchange Server 2013 SP1_

_**上次修改主題的時間：**2015-03-09_

自動重新植入或 AutoReseed，是屬於功能正常的系統管理員導向動作以回應磁碟故障、 資料庫損毀事件或必須重新植入資料庫複本的其他問題的取代功能。AutoReseed 的設計目的自動在使用已佈建的備用磁碟系統上的磁碟故障後還原資料庫的備援。

## Autoreseed 的概觀

AutoReseed 組態使用標準化的儲存呈現架構，由系統管理員選擇起點。AutoReseed 幾乎是在磁碟機故障後迅速還原備援。此動作涵蓋使用掛接點預先對應一組磁碟區 (包括備用磁碟區) 和資料庫。磁碟故障時作業系統無法再使用磁碟或磁碟不再可以寫入，系統會配置備用磁碟區，並自動重新植入受影響的資料庫副本。

1.  Microsoft Exchange複寫服務會定期掃描具有 FailedAndSuspended 狀態的副本。如果設定為 AutoReseed 的磁碟區上的所有資料庫副本 FailedandSuspended 狀態 15 連續分鐘，起始 AutoReseed 工作流程。

2.  AutoReseed 會嘗試與傳來每一次嘗試 5 分鐘睡眠繼續失敗並已擱置副本最多三倍。有時，繼續執行 FailedandSuspended 資料庫副本之後，請複製仍會保留在 「 失敗 」 狀態中。就會發生這個各種理由，讓此步驟設計來處理這些案例;AutoReseed 自動將擱置保留執行的工作流程的 10 個連續分鐘已失敗的資料庫副本。如果暫停及繼續動作不會導致狀況良好的資料庫副本，工作流程會繼續執行。

3.  時都會使用該狀態的複本，便會執行一些必要條件檢查。例如，它會確認備用磁碟可用，在相同的磁碟區，並在符合所需的命名慣例的適當位置中所要設定資料庫和及其記錄檔。

4.  如果必要條件檢查順利通過，Microsoft Exchange 複寫服務內的功能會配置、 重新對應及格式化備用磁碟根據下表中時間表的 Disk reclaimer 功能。AutoReseed 會嘗試將指派給備用磁碟區多達 5 次睡眠每個 try 傳來的 1 小時。

5.  指派一個備用磁碟後，AutoReseed 會執行使用植入交換器 SafeDeleteExistingFiles InPlaceSeed 作業。已在受影響的磁碟的所有資料庫已重新植都入使用之資料庫的主動副本作為植入來源。

6.  完成植入操作之後，Microsoft Exchange 複寫服務會驗證新植入的副本是否正常。

一旦完所有的重試次數，會停止工作流程。 如果 3 天後資料庫副本仍然是 FailedandSuspended、 工作流程狀態會重設並重新啟動步驟 1 中。 此重設/繼續行為會很有用 （而且刻意） 後可能需要幾天來取代失敗的磁碟控制器、 等。

此時，如果該故障屬於磁碟故障，將需要操作員或系統管理員手動介入來移除並更換故障的磁碟，然後將更換的磁碟重新設定為備用磁碟。

AutoReseed 是透過使用 DAG 的三個屬性來進行設定。其中兩個屬性是指兩個使用中的掛接點。Exchange 2013 運用了 Windows Server 容許每個磁碟區擁有多個掛接點的功能。*AutoDagVolumesRootFolderPath* 屬性是指包含所有可用磁碟區的掛接點。這包含管理資料庫和備用磁碟區的磁碟區。*AutoDagDatabasesRootFolderPath* 屬性是指包含資料庫的掛接點。第三個 DAG 屬性 *AutoDagDatabaseCopiesPerVolume* 用於設定每個磁碟區資料庫副本的數目。

下列說明 AutoReseed 設定的範例。

**AutoReseed 組態範例**

![自動重新植入組態範例](images/Dn789209.e3af7306-f5b4-4ec4-9ccf-222ec452699b(EXCHG.150).gif "自動重新植入組態範例")

在此範例中，具有三個磁碟區，其中兩個將包含資料庫 (VOL1 和 VOL2)，其中一個是格式化的空白備用磁碟區 (VOL3)。

AutoReseed 的設定方式：

1.  所有三個磁碟區都掛接於單一掛接點下。此範例使用掛接點 C:\\ExchVols。這表示此目錄用於儲存 Exchange 資料庫。

2.  信箱資料庫的根目錄以另一個掛接點掛接。此範例使用掛接點 C:\\ExchDBs。接著建立目錄結構，以便為資料庫建立上層目錄，並在上層目錄下建立兩個子目錄：一個資料庫檔案，一個用於記錄檔。

3.  資料庫即建立完成。上述的範例說明每個磁碟區使用單一資料庫的簡單設計。因此，在 VOL1 上有三個目錄：上層目錄和兩個子目錄 (一個用於 MDB1 的資料庫檔案，一個用於其記錄)。雖然在範例圖像中未列出，但在 VOL2 上也會有三個目錄：上層目錄、上層目錄底下用於 MDB2 資料庫檔案的目錄，以及一個用於其記錄檔的目錄。

在此組態中，如果 MDB1 或 MDB2 故障，故障資料庫的副本會自動重新植入到 VOL3。

## Disk Reclaimer

可配置和格式化備用磁碟的 AutoReseed 元件稱為 *Disk Reclaimer*。Disk Reclaimer 元件會自動格式化備用磁碟，以準備依不同的間隔來重新植入，視磁碟的狀態而定。為了讓 Disk Reclaimer 將磁碟格式化，必須符合某些條件：

  - 必須啟用 Disk Reclaimer。依預設會啟用，但可使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\)) 來停用。

  - 磁碟區在磁碟區根路徑中必須有掛接點 (根據預設，C:\\ExchangeVolumes)。

  - 磁碟區在資料庫磁碟區路徑中不能有任何掛接點 (根據預設，C:\\ExchangeDatabases)。

  - 如果磁碟區包含任何檔案，則 24 小時內不可使用任何檔案。

除了上述條件，Disk Reclaimer 一天只會嘗試將指定的磁碟區格式化一次。下表說明 Disk Reclaimer 的格式化行為。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>磁碟和資料庫副本的狀態</th>
<th>格式化間隔</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>磁碟未格式化，或是已格式化但空白，或是已格式化但包含 24 小時內未使用的檔案，而且本機 Active Directory 站台有良好的主動資料庫副本可做為植入來源。</p></td>
<td><p>1 天</p></td>
</tr>
<tr class="even">
<td><p>磁碟未格式化，或是已格式化但空白，或是已格式化但包含 24 小時內未使用的檔案，但本機 Active Directory 站台沒有良好的主動資料庫副本可做為植入來源。</p></td>
<td><p>2 天</p></td>
</tr>
<tr class="odd">
<td><p>磁碟未格式化，或是已格式化但空白，或是已格式化但包含 24 小時內未使用的檔案，而且本機 Active Directory 站台有良好的主動資料庫副本可做為植入來源，但資料庫檔案 (EDB 檔) 和記錄檔之外還有不明的檔案。</p></td>
<td><p>2 週</p></td>
</tr>
<tr class="even">
<td><p>磁碟未格式化，或是已格式化但空白，或是已格式化但包含 24 小時內未使用的檔案，而且本機 Active Directory 站台有良好的主動資料庫副本可做為植入來源，但資料庫的一或多個資料庫檔案 (EDB 檔) 不存在 Active Directory 中。</p></td>
<td><p>2 週</p></td>
</tr>
</tbody>
</table>

