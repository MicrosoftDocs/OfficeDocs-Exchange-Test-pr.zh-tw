---
title: '監視資料庫可用性群組: Exchange 2013 Help'
TOCTitle: 監視資料庫可用性群組
ms:assetid: f5bdfd6e-e93c-4d96-8bc2-548750d51930
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351258(v=EXCHG.150)
ms:contentKeyID: 50474603
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 監視資料庫可用性群組

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以使用本主題中的詳細資料監視的健康狀況和狀態的信箱資料庫副本的資料庫可用性群組 (DAGs) 收集診斷資訊，以及如何設定監控臨界值的低磁碟空間。

## Get-MailboxDatabaseCopyStatus Cmdlet

您可以使用 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-tw/library/dd298044\(v=exchg.150\)) 指令程式來檢視信箱資料庫副本的狀態資訊。此指令程式可讓您檢視特定資料庫的所有副本資訊、特定伺服器的特定副本資訊，或伺服器的所有資料庫副本資訊。下表說明信箱資料庫可能的副本狀態值。

### 資料庫副本狀態

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>資料庫副本狀態</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>失敗</p></td>
<td><p>因為信箱資料庫副本未擱置且無法複製或重新顯示記錄檔，所以信箱資料庫副本的狀態為「失敗」。當狀態為「失敗」且未擱置時，系統會定期檢查導致副本狀態變更為「失敗」的問題是否已解決。當系統偵測到問題已解決且沒有其他問題，副本狀態會自動變更為「正常」。</p></td>
</tr>
<tr class="even">
<td><p>植入</p></td>
<td><p>已植入信箱資料庫副本、信箱資料庫副本的內容索引，或是兩者皆已植入。成功完成植入時副本狀態應變更為正在初始化。</p></td>
</tr>
<tr class="odd">
<td><p>SeedingSource</p></td>
<td><p>信箱資料庫副本正被用來作為資料庫副本植入作業的來源。</p></td>
</tr>
<tr class="even">
<td><p>已擱置</p></td>
<td><p>因為系統管理員執行 <strong>Suspend-MailboxDatabaseCopy</strong> 指令程式，手動擱置資料庫副本，所以信箱資料庫副本的狀態為「已擱置」。</p></td>
</tr>
<tr class="odd">
<td><p>正常</p></td>
<td><p>信箱資料庫副本成功複製並重新顯示記錄檔，或已成功複製並重新顯示所有可用的記錄檔。</p></td>
</tr>
<tr class="even">
<td><p>ServiceDown</p></td>
<td><p>Microsoft Exchange 複寫服務無法在主控信箱資料庫副本的伺服器上使用或執行。</p></td>
</tr>
<tr class="odd">
<td><p>初始化</p></td>
<td><p>當已建立信箱資料庫副本、Microsoft Exchange 複寫服務開始或剛開始，以及從「已擱置」、「服務關閉」、「失敗」、「植入」、「單一頁面還原」轉換為其他狀態期間，信箱資料庫副本的狀態將為「正在初始化」。在此狀態下，系統會驗證資料庫和記錄資料流的狀態是否一致。在大部分情況下，副本狀態會維持在「正在初始化」的狀態約 15 秒，但在任何情況下，通常維持在此狀態的時間不應超過 30 秒。</p></td>
</tr>
<tr class="even">
<td><p>重新同步處理</p></td>
<td><p>信箱資料庫副本及其記錄檔已經和資料庫的主動副本比對過，以檢查兩份副本之間的任何分歧。副本狀態會維持在此狀態，直到偵測到分歧或分歧解決為止。</p></td>
</tr>
<tr class="odd">
<td><p>已裝載</p></td>
<td><p>主動副本為線上並接受用戶端連線。只有信箱資料庫的主動副本可以有「已裝載」的副本狀態。</p></td>
</tr>
<tr class="even">
<td><p>已卸載</p></td>
<td><p>主動副本為離線且不接受用戶端連線。只有信箱資料庫的主動副本可以有「已卸載」的副本狀態。</p></td>
</tr>
<tr class="odd">
<td><p>裝載中</p></td>
<td><p>主動副本正在進入線上，並且尚未接受用戶端連線。只有信箱資料庫的主動副本可以有「裝載中」的副本狀態。</p></td>
</tr>
<tr class="even">
<td><p>卸載中</p></td>
<td><p>主動副本即將離線並終止用戶端連線。只有信箱資料庫的主動副本可以有「卸載中」的副本狀態。</p></td>
</tr>
<tr class="odd">
<td><p>DisconnectedAndHealthy</p></td>
<td><p>信箱資料庫副本不再連線至主動資料庫副本，並且在中斷連線時其狀態為「正常」。此狀態表示資料庫副本與其來源資料庫副本的連接性。來源副本和目標資料庫副本之間發生 DAG 網路失敗時即可能報告此狀態。</p></td>
</tr>
<tr class="even">
<td><p>DisconnectedAndResynchronizing</p></td>
<td><p>信箱資料庫副本不再連線至主動資料庫副本，並且在中斷連線時其狀態為「重新同步處理」。此狀態表示資料庫副本與其來源資料庫副本的連接性。來源副本和目標資料庫副本之間發生 DAG 網路失敗時即可能報告此狀態。</p></td>
</tr>
<tr class="odd">
<td><p>FailedAndSuspended</p></td>
<td><p>由於偵測到失敗，並且明確需要系統管理員的介入來解決失敗，所以系統同時設定了「失敗」和「已擱置」狀態。例如，如果系統在作用中信箱資料庫和資料庫副本之間偵測到無法復原的分歧。不像「失敗」狀態，系統不會定期檢查問題是否已解決並自動復原。而是在資料庫副本可以轉換為正常狀態之前，由系統管理員介入來解決失敗的根本原因。</p></td>
</tr>
<tr class="even">
<td><p>SinglePageRestore</p></td>
<td><p>此狀態表示信箱資料庫副本發生單一頁面還原操作。</p></td>
</tr>
</tbody>
</table>


**Get-MailboxDatabaseCopyStatus** Cmdlet 也會傳回使用中複寫網路的詳細資料，包括 *IncomingLogCopyingNetwork* (會針對被動資料庫副本來傳回) 和 *OutgoingConnections* (會針對有多份副本的主動資料庫來傳回)，以及任何被當成資料庫植入作業來源的資料庫副本。只有對於處於檔案模式複寫的資料庫副本，才會提供外寄連線資訊。 對於處於封鎖模式複寫的資料庫副本，並不會提供外寄連線資訊。

## Get-MailboxDatabaseCopyStatus 範例

下列範例使用 **Get-MailboxDatabaseCopyStatus** 指令程式。每一個範例都會將結果以管線傳送至 **Format-List** 指令程式，以便以清單格式顯示輸出。

本範例傳回 DB2 資料庫所有複本的狀態資訊。

    Get-MailboxDatabaseCopyStatus -Identity DB2 | Format-List

本範例傳回信箱伺服器 MBX2 上所有資料庫複本的狀態。

    Get-MailboxDatabaseCopyStatus -Server MBX2 | Format-List

此範例傳回本機 Mailbox Server 上所有資料庫副本的狀態。

    Get-MailboxDatabaseCopyStatus -Local | Format-List

如需使用 **Get-MailboxDatabaseCopyStatus** 指令程式的相關資訊，請參閱 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-tw/library/dd298044\(v=exchg.150\))。

## Test-ReplicationHealth Cmdlet

您可以使用 [Test-ReplicationHealth](https://technet.microsoft.com/zh-tw/library/bb691314\(v=exchg.150\)) 指令程式來檢視信箱資料庫副本的連續複寫狀態資訊。此指令程式可用來檢查複寫和重新顯示的各個部分，以提供 DAG 中特定 Mailbox Server 的完整概觀。

**Test-ReplicationHealth** 指令程式旨在用來主動監視連續複寫和連續複寫管線、Active Manager 的可用性，以及基礎叢集服務、仲裁及網路元件的健全狀況和狀態。可在本機或在遠端針對 DAG 中任何的信箱伺服器執行。**Test-ReplicationHealth** 指令程式會執行下表所列出的測試。

### Test-ReplicationHealth 指令程式測試

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>測試名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ClusterService</p></td>
<td><p>驗證在指定的 DAG 成員上是否正在執行叢集服務並且可以存取，若沒有指定任何 DAG 成員，則驗證本機伺服器。</p></td>
</tr>
<tr class="even">
<td><p>ReplayService</p></td>
<td><p>驗證在指定的 DAG 成員上是否正在執行 Microsoft Exchange 複寫服務並且可以存取，若沒有指定任何 DAG 成員，則驗證本機伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>ActiveManager</p></td>
<td><p>驗證在指定的 DAG 成員上執行的 Active Manager 執行個體 (若沒有指定任何 DAG 成員，則為本機伺服器)，其角色是有效的 (主要、次要或獨立)。</p></td>
</tr>
<tr class="even">
<td><p>TasksRpcListener</p></td>
<td><p>驗證在指定的 DAG 成員上是否正在執行工作遠端程序呼叫 (RPC) 伺服器並且可以存取，若沒有指定任何 DAG 成員，則驗證本機伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>TcpListener</p></td>
<td><p>驗證在指定的 DAG 成員上是否正在執行 TCP 記錄複製接聽程式並且可以存取，若沒有指定任何 DAG 成員，則驗證本機伺服器。</p></td>
</tr>
<tr class="even">
<td><p>ServerLocatorService</p></td>
<td><p>驗證在 DAG 成員上和在 Client Access Server 上是否有會在 Active Directory 和 Active Manager 中執行查閱來判斷使用者的信箱資料庫是在哪裡作用的 Active Manager 用戶端/伺服器程序。</p></td>
</tr>
<tr class="odd">
<td><p>DagMembersUp</p></td>
<td><p>驗證所有 DAG 成員是否可以使用、執行和存取。</p></td>
</tr>
<tr class="even">
<td><p>ClusterNetwork</p></td>
<td><p>驗證在指定的 DAG 成員 (若沒有指定任何 DAG 成員，則為本機伺服器) 上找到的所有叢集管理網路是否皆可用。</p></td>
</tr>
<tr class="odd">
<td><p>QuorumGroup</p></td>
<td><p>驗證預設的叢集群組 (仲裁群組) 的狀態為正常且為線上。</p></td>
</tr>
<tr class="even">
<td><p>FileShareQuorum</p></td>
<td><p>驗證見證伺服器、見證目錄和 DAG 的共用設定是否皆可存取。</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseRedundancy</p></td>
<td><p>驗證在指定的 DAG 成員 (如果未指定 DAG 成員，則為本機伺服器) 上是否至少有一個狀況良好的可用資料庫副本。</p></td>
</tr>
<tr class="even">
<td><p>DatabaseAvailability</p></td>
<td><p>驗證資料庫在指定的 DAG 成員 (如果未指定 DAG 成員，則為本機伺服器) 上是否有足夠的可用性。</p></td>
</tr>
<tr class="odd">
<td><p>DBCopySuspended</p></td>
<td><p>檢查在指定的 DAG 成員上所有信箱資料庫副本的狀態是否皆為「已擱置」，若沒有指定任何 DAG 成員，則檢查本機伺服器。</p></td>
</tr>
<tr class="even">
<td><p>DBCopyFailed</p></td>
<td><p>檢查在指定的 DAG 成員上所有信箱資料庫副本的狀態是否皆為「失敗」，若沒有指定任何 DAG 成員，則檢查本機伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>DBInitializing</p></td>
<td><p>檢查在指定的 DAG 成員上所有信箱資料庫副本的狀態是否皆為「正在初始化」，若沒有指定任何 DAG 成員，則檢查本機伺服器。</p></td>
</tr>
<tr class="even">
<td><p>DBDisconnected</p></td>
<td><p>檢查在指定的 DAG 成員上所有信箱資料庫副本的狀態是否皆為「已中斷連線」，若沒有指定任何 DAG 成員，則檢查本機伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>DBLogCopyKeepingUp</p></td>
<td><p>驗證在指定的 DAG 成員 (若沒有指定任何 DAG 成員，則驗證本機伺服器) 上資料庫被動副本的記錄檔複製和檢查是否可跟得上被動副本上的記錄檔產生活動。</p></td>
</tr>
<tr class="even">
<td><p>DBLogReplayKeepingUp</p></td>
<td><p>驗證在指定的 DAG 成員 (若沒有指定任何 DAG 成員，則驗證本機伺服器) 上資料庫被動副本的重新顯示活動是否可跟得上記錄檔複製和檢查活動。</p></td>
</tr>
</tbody>
</table>


## Test-ReplicationHealth 範例

這個範例使用 **Test-ReplicationHealth** 指令程式來測試 Mailbox Server MBX1 的複寫狀況。

    Test-ReplicationHealth -Identity MBX1

## Crimson 通道事件記錄

Windows 包含兩個類別的事件記錄：Windows 記錄與「應用程式及服務」記錄。Windows 記錄類別包含可於舊版 Windows 使用的事件記錄：應用程式、 安全性和系統事件記錄。也包含兩個新記錄：「安裝」記錄與 ForwardedEvents 記錄。Windows 記錄的目的是從舊版應用程式和套用到整個系統的事件儲存事件。

「應用程式及服務」記錄是新的事件記錄類別。這些記錄儲存單一應用程式或元件中的事件，而非可能影響整個系統的事件。事件記錄的這個新類別稱為應用程式的Crimson 通道。

「應用程式及服務」記錄類別包含四個子類型：「系統管理」、「操作」、「分析」和「偵錯」記錄。如果您使用事件記錄來疑難排解問題，則「系統管理」記錄中的事件特別有用。「系統管理」記錄中的事件應提供您如何回應事件的指引。「操作」記錄中的事件也相當有用，但可能需要更多解譯。「系統管理」與「偵錯」記錄難以使用。「分析」記錄 (預設為隱藏並停用) 儲存用於追蹤問題的事件，經常記錄著大量事件。「偵錯」記錄供開發人員於偵錯應用程式時使用。

Exchange 2013 將事件記錄到「應用程式及服務」記錄區的Crimson 通道內。您可以執行下列步驟來檢視這些通道：

1.  開啟 \[事件檢視器\]。

2.  在主控台樹狀目錄中，瀏覽至 \[應用程式及服務記錄\] \> \[Microsoft\] \> \[Exchange\]。

3.  \[ **Exchange**\] 下選取 \[crimson 通道，例如**\[highavailability\]**或**\[MailboxDatabaseFailureItems**查看 DAG 和資料庫副本相關的事件，或**ActiveMontoring**或**ManagedAvailability**查看事件相關的受管理的可用性。

HighAvailability 通道包含與啟動和關閉 Microsoft Exchange 複寫服務相關的事件，以及 Microsoft Exchange 複寫服務內執行的元件，例如，Active Manager、第三方同步處理複寫 API、工作 RPC 伺服器、TCP 接聽程式和磁碟區陰影複製服務 (VSS) 編寫器。Active Manager 也會使用 HighAvailability 通道來記錄與 Active Manager 角色監視相關的事件和資料庫動作事件，例如，資料庫裝載操作和記錄檔截斷，以及記錄與 DAG 基礎叢集相關的事件。

MailboxDatabaseFailureItems 通道可用來記錄影響複寫信箱資料庫失敗的所有相關事件。

ActiveMonitoring 通道包含受管理的可用性探查、 監視器及回應程式的定義和結果事件。

ManagedAvailability 通道包含復原動作記錄和結果和相關的事件。

## 低磁碟空間的監視器

Exchange 2013受管理可用性監視器百系統評量和元件的每分鐘，包括在信箱伺服器角色所使用的磁碟區上的可用磁碟空間量。前Exchange 2013 Service Pack 1 (SP1)、 Exchange 監視所有的本機磁碟區，包括不包含任何資料庫或記錄檔磁碟區上的可用空間。Sp1 和更新版本、 受監控的包含 Exchange 資料庫和記錄檔磁碟區。Sp1、 低磁碟區空間監視器的預設臨界值為 200 GB。Exchange 2013 6 和更新版本的累計更新、 中的預設臨界值為 180 GB。Sp1 和更新版本、 您可以設定臨界值新增下列 DWORD 登錄值 （以 mb 為單位） 您要自訂每個信箱伺服器上：

路徑： **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters**

值： *SpaceMonitorLowSpaceThresholdInMB*

若要設定臨界值設定為 100 GB 的範例，您會設定下列登錄值：

**REG\_DWORD 186a0 (100000)**

設定或之後修改上述登錄值，您必須重新啟動 Microsoft Exchange DAG 管理服務，讓變更生效。

## CollectOverMetrics.ps1 指令碼

Exchange 2013 包含稱為 CollectOverMetrics.ps1 的指令碼，您可以在 Scripts 資料夾內找到這個指令碼。CollectOverMetrics.ps1 會讀取 DAG 成員事件日誌，以收集一段特定時間內的資料庫作業相關資訊 (例如資料庫裝載、移動和轉換)。此指令碼會記錄每一項作業的下列資訊：

  - 資料庫的識別碼

  - 作業開始和結束的時間

  - 作業開始和完成時用來裝載資料庫的伺服器

  - 執行作業的原因

  - 作業是否執行成功，若是作業失敗時則顯示錯誤詳細資料

此指令碼會以每列一項作業的方式將這些資訊寫入 .csv 檔案中。它會為每個 DAG 寫入一個個別的 .csv 檔案。

指令碼支援可讓您自訂指令碼行為和輸出的參數。例如，您可以使用 *Database* 或 *ReportFilter* 參數將產生的結果限定為指定的子集。摘要 HTML 報告中只會包含符合這些篩選器的作業。下表列出可用的參數。

### CollectOverMetrics.ps1 指令碼參數

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DatabaseAvailabilityGroup</em></p></td>
<td><p>指定您想從其中收集度量資訊的 DAG 名稱。若省略此參數，會使用本機伺服器為其成員的 DAG。您可以使用萬用字元從多個 DAG 收集資訊並提供其相關報告。</p></td>
</tr>
<tr class="even">
<td><p><em>Database</em></p></td>
<td><p>提供需產生報告的資料庫清單。支援萬用字元，例如，<code>-Database:&quot;DB1&quot;,&quot;DB2&quot;</code> 或 <code>-Database:&quot;DB*&quot;</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>指定所要報告之時段的持續時間。指令碼只會收集在這段時間內記錄的事件。因此，指令碼可能會擷取一部分的作業記錄 (例如，只有該時段開始時的作業結尾或相反)。如果沒有指定 <em>StartTime</em> 也沒有指定 <em>EndTime</em>，指令碼會預設為過去 24 小時。如果只指定其中一個參數，此時段將為於指定之時間開始或結束的 24 小時。</p></td>
</tr>
<tr class="even">
<td><p><em>EndTime</em></p></td>
<td><p>指定所要報告之時段的持續時間。指令碼只會收集在這段時間內記錄的事件。因此，指令碼可能會擷取一部分的作業記錄 (例如，只有該時段開始時的作業結尾或相反)。如果沒有指定 <em>StartTime</em> 也沒有指定 <em>EndTime</em>，指令碼會預設為過去 24 小時。如果只指定其中一個參數，此時段將為於指定之時間開始或結束的 24 小時。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>指定用來儲存事件處理結果的資料夾。若省略此參數，則會使用 Scripts 資料夾。指定此參數時，指令碼會取得指令碼所產生的 .csv 檔案清單，並使用它們當作產生摘要 HTML 報告的資料來源。此報告與使用 -GenerateHtmlReport 選項所產生的報告相同。檔案可以在許多不同時間 (甚至是時間重疊) 橫跨多個 DAG 而產生，而且指令碼可將它們的所有資料合部合併在一起。</p></td>
</tr>
<tr class="even">
<td><p><em>GenerateHtmlReport</em></p></td>
<td><p>指定讓指令碼收集它曾記錄的所有資訊、按作業類型將資料分組，然後再產生包含每個分組之統計資料的 HTML 檔案。此報告包括各分組的作業總數、失敗的作業數目，以及每一組所花費的時間。報告中也包含造成作業失敗之錯誤類型的細目。</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowHtmlReport</em></p></td>
<td><p>指定 HTML 產生的報表於產生後應以 Web 瀏覽器顯示。</p></td>
</tr>
<tr class="even">
<td><p><em>SummariseCsvFiles</em></p></td>
<td><p>指定讓指令碼從指令碼先前產生的現有 .csv 檔案讀取資料，然後再使用這項資料產生與 <em>GenerateHtmlReport</em> 參數產生之報告類似的摘要報告。</p></td>
</tr>
<tr class="odd">
<td><p><em>ActionType</em></p></td>
<td><p>指定指令碼應收集的操作動作類型。這個參數的值為 <code>Move</code>、<code>Mount</code>、<code>Dismount</code> 和 <code>Remount</code>。<code>Move</code> 值是指每次資料庫變更其作用中的伺服器時 (不論是受控制移動或容錯移轉) 所進行的動作。<code>Mount</code>、<code>Dismount</code> 和 <code>Remount</code> 值則是指資料庫變更其裝載的狀態，但並未移動至其他電腦。</p></td>
</tr>
<tr class="even">
<td><p><em>ActionTrigger</em></p></td>
<td><p>指定指令碼應收集哪些系統管理作業。這個參數的值為 <code>Admin</code> 或 <code>Automatic</code>。Automatic 動作是系統自動執行的動作 (例如，伺服器離線時的容錯移轉)。Admin 動作是系統管理員使用 Exchange 管理命令介面或 Exchange 系統管理中心執行的任何動作。</p></td>
</tr>
<tr class="odd">
<td><p><em>RawOutput</em></p></td>
<td><p>指定讓指令碼將已寫入至 .csv 檔案的結果，直接寫入輸出資料流中，就和使用 write-output 一樣。接著便可將這項資訊傳送到其他命令。</p></td>
</tr>
<tr class="even">
<td><p><em>IncludedExtendedEvents</em></p></td>
<td><p>指定讓指令碼收集事件，而收集的事件提供裝載資料庫所花時間的診斷詳細資料。如果伺服器的應用程式事件日誌很大，這個階段可能非常耗時。</p></td>
</tr>
<tr class="odd">
<td><p><em>MergeCSVFiles</em></p></td>
<td><p>指定讓指令碼取得包含每一項作業相關資料的所有 .csv 檔案，並將它們合併成單一 .csv 檔案。</p></td>
</tr>
<tr class="even">
<td><p><em>ReportFilter</em></p></td>
<td><p>指定應使用出現在 .csv 檔案中的欄位將篩選器套用到作業。這個參數使用的格式與 <code>Where</code> 作業相同，也就是將每個元素設定為 <code>$_</code>，並傳回布林值。例如：<code>{$_DatabaseName -notlike &quot;Mailbox Database*&quot;}</code> 可用來在報告中排除預設資料庫。</p></td>
</tr>
</tbody>
</table>


## CollectOverMetrics.ps1 範例

下列範例會收集 DAG DAG1 中符合 DB\* (包含萬用字元) 的所有資料庫度量資訊。收集度量資訊之後，會產生並顯示 HTML 報告。

    CollectOverMetrics.ps1 -DatabaseAvailabilityGroup DAG1 -Database:"DB*" -GenerateHTMLReport -ShowHTMLReport

下列範例示範摘要 HTML 報告可以使用的篩選方法。第一種範例使用 *Database* 參數取得資料庫名稱的清單，讓摘要報告中只包含這些資料庫的相關資料。後面兩個範例則使用 *ReportFilter* 選項。最後一個範例會篩選出所有的預設資料庫。

    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -Database MailboxDatabase123,MailboxDatabase456
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { $_.DatabaseName -notlike "Mailbox Database*" }
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { ($_.ActiveOnStart -like "ServerXYZ*") -and ($_.ActiveOnEnd -notlike "ServerXYZ*") }

## CollectReplicationMetrics.ps1 指令碼

另一個包含在 Exchange 2013 內的狀況度量指令碼是 CollectReplicationMetrics.ps1。這個指令碼在執行時即時收集度量資訊，所以提供了一種主動形式的監視。CollectReplicationMetrics.ps1 會從與資料庫複寫相關的效能計數器收集資料。此指令碼會收集多個信箱伺服器的計數器資料、將每部伺服器的資料寫入 .csv 檔案，然後報告所有資料的各種統計資料 (例如每個副本失敗或擱置的時間長度、平均的複製佇列長度或重新顯示佇列長度，或是副本不符合容錯移轉準則的時間長度)。

您可以個別指定伺服器，或是指定整個 DAG。您可執行指令碼讓它先收集資料再產生報告，也可以讓它只收集資料，或是只報告已經收集的資料。您可以指定資料的取樣頻繁，以及收集資料的總時間長度。

從每部伺服器收集的資料都會寫入到名為 **CounterData.\<ServerName\>.\<TimeStamp\>.csv** 的檔案中。摘要報告會寫入名稱為 \[HaReplPerfReport.\<DAGName\>.\<TimeStamp\>.csv\] 的檔案，而如果執行指令碼時沒有指定 *DagName* 參數，則會寫入名稱為 \[HaReplPerfReport.\<TimeStamp\>.csv\] 的檔案。

指令碼會啟動 Windows PowerShell 工作來收集每部伺服器的資料。這些工作會在整段資料收集期間執行。如果您指定的伺服器數目很多，這個程序可能會使用大量的記憶體。在這個程序的最後一個階段，也就是將資料處理成摘要報告時，也可能會因為大量的資料而耗費相當多的時間。您可以在某部電腦上執行收集階段，然後將資料複製到其他電腦來進行處理作業。

CollectReplicationMetrics.ps1 指令碼支援可讓您自訂指令碼行為和輸出的參數。下表列出可用的參數。

### CollectReplicationMetrics.ps1 指令碼參數

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>指定您想從其中收集度量資訊的 DAG 名稱。若省略此參數，會使用本機伺服器為其成員的 DAG。</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseNames</em></p></td>
<td><p>提供需產生報告的資料庫清單。支援使用萬用字元，例如，<code>-DatabaseNames:&quot;DB1&quot;,&quot;DB2&quot;</code> 或 <code>-DatabaseNames:&quot;DB*&quot;</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>指定用來儲存事件處理結果的資料夾。若省略此參數，則會使用 Scripts 資料夾。</p></td>
</tr>
<tr class="even">
<td><p><em>Duration</em></p></td>
<td><p>指定收集程序應執行的時間量。一般的值為一到三個小時。只有在每次取樣的間隔時間較長，或是排定工作執行一連串較短的工作時，才能使用較長的時間。</p></td>
</tr>
<tr class="odd">
<td><p><em>Frequency</em></p></td>
<td><p>指定資料度量資訊的收集頻率。一般的值為 30 秒、一分鐘或五分鐘。在正常情況下，如果間隔時間比這些值還短，各個取樣之間並不會出現顯著的變化。</p></td>
</tr>
<tr class="even">
<td><p><em>Servers</em></p></td>
<td><p>指定統計資料收集來源之伺服器的識別碼。您可以指定任何值，包括萬用字元或 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><em>SummariseFiles</em></p></td>
<td><p>指定要產生摘要報告的 .csv 檔案清單。這些檔案是名為 <strong>CounterData.&lt;CounterData&gt;*</strong>，且由 CollectReplicationMetrics.ps1 指令碼產生的檔案。</p></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>指定指令碼執行的處理階段。您可以使用下列值：</p>
<ul>
<li><p><code>CollectAndReport</code>   此為預設值。這個值代表指令碼應該會收集伺服器的資料，然後再處理資料來產生摘要報告。</p></li>
<li><p><code>CollectOnly</code>   這個值代表指令碼應該只會收集資料，而不會產生報告。</p></li>
<li><p><code>ProcessOnly</code>   這個值代表指令碼應該會從一組 .csv 檔案匯入資料，並處理資料來產生摘要報告。<em>SummariseFiles</em> 參數可用來為指令碼提供要處理的檔案清單。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MoveFilestoArchive</em></p></td>
<td><p>指定指令碼應該在處理完成後，將檔案移到壓縮資料夾。</p></td>
</tr>
<tr class="even">
<td><p><em>LoadExchangeSnapin</em></p></td>
<td><p>指定指令碼應該載入命令介面命令。當指令碼需要從命令介面外部執行時 (例如在已排程的工作中)，可以使用此參數。</p></td>
</tr>
</tbody>
</table>


## CollectReplicationMetrics.ps1 範例

下列範例會從 DAG DAG1 中的所有伺服器收集一個小時的資料量，每隔一分鐘取樣一次，然後再產生摘要報告。此外還會使用 *ReportPath* 參數，讓指令碼將所有的檔案放在目前的目錄中。

    CollectReplicationMetrics.ps1 -DagName DAG1 -Duration "01:00:00" -Frequency "00:01:00" -ReportPath

下列範例會從符合 CounterData\* 的所有檔案讀取資料，然後再產生摘要報告。

    CollectReplicationMetrics.ps1 -SummariseFiles (dir CounterData*) -Mode ProcessOnly -ReportPath

