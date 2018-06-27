---
title: '管理信箱還原要求: Exchange 2013 Help'
TOCTitle: 管理信箱還原要求
ms:assetid: 8e668a52-c601-4d96-a51c-ab60267e1321
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ863437(v=EXCHG.150)
ms:contentKeyID: 50554030
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理信箱還原要求

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

信箱還原要求可用來還原已中斷連線的信箱。中斷連線的信箱已在 Exchange 信箱資料庫與 Active Directory 使用者帳戶沒有關聯的信箱。信箱成為中斷時所要停用、 刪除或移至另一個資料庫。如需詳細資訊，請參閱[中斷連線的信箱](disconnected-mailboxes-exchange-2013-help.md)。

中斷連線的信箱保留信箱資料庫中的信箱資料庫的已刪除的信箱保留設定中指定的工期。根據預設，中斷連線的信箱會保留 30 天。此保留期間可以 （複製） 到現有的信箱會還原已刪除的信箱的內容。本主題說明如何使用命令介面來管理信箱還原要求。

如需與中斷連線信箱相關的其他管理工作，請參閱下列主題：

[停用或刪除信箱](disable-or-delete-a-mailbox-exchange-2013-help.md)

[連線已停用的信箱](connect-a-disabled-mailbox-exchange-2013-help.md)

[連線或還原已刪除的信箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

[還原虛刪除信箱](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

[永久刪除信箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱還原要求」項目。

  - 本主題中的程序只可以在命令介面中執行。您無法使用 EAC 來管理信箱還原要求。

  - 若要顯示所有信箱還原請求的 *Identity* 屬性值，執行下列指令。
    
        Get-MailboxRestoreRequest | Format-Table Identity
    
    執行此主題內的程序時，您可以使用此辨識值以指定特定信箱還原請求。

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

## 使用命令介面檢視還原請求屬性

您可以檢視信箱還原請求屬性，屬性提供有關信箱還原請求狀態的基本資訊。

若要顯示請單與所有信箱還原請求的 *Identity* 屬性值，執行下列指令。

    Get-MailboxRestoreRequest | Format-Table Identity

您可以使用辨識以取得有關特定信箱還原請求的資訊。

此範例傳回使用 *Identity* 參數的「Pilar Pinilla \\MailboxRestore 」還原請求之狀態。

    Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore"

此範例傳回 Pilar Pinilla 目標信箱第二次還原請的所有資訊。

    Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1" | Format-List

此範例會傳回正從來源資料庫 MBD01 還原的還原要求狀態。

    Get-MailboxRestoreRequest -SourceDatabase MBD01

此範例傳回目前進行中的所有還原請求。

    Get-MailboxRestoreRequest -Status InProgress

其他有用的狀態包括 `Queued`、`Completed`、`Suspended` 以及 `Failed`。

此範例傳回已暫停的所有還原請求。

    Get-MailboxRestoreRequest -Suspend $true

如需詳細的語法及參數資訊，請參閱 [Get-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829907\(v=exchg.150\))。

## Get-MailboxRestoreRequest 輸出

根據預設， **Get-MailboxRestoreRequest**指令程式會傳回名稱要求、 目標信箱正在還原的資料，並要求的狀態。下表列出如果您將傳送到**Format-List**指令程式指令程式會傳回有用的資訊。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SourceDatabase</code></p></td>
<td><p>指定包含正還原的中斷連線信箱之資料庫。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetMailbox</code></p></td>
<td><p>指定要將資料還原到哪個信箱中。</p></td>
</tr>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>指定要求的名稱。</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>指定 Microsoft Exchange 信箱複寫服務 (MRS) 在哪個資料庫上儲存要求的詳細狀態。</p></td>
</tr>
<tr class="odd">
<td><p><code>Status</code></p></td>
<td><p>指定要求的狀態。</p></td>
</tr>
<tr class="even">
<td><p><code>Suspend</code></p></td>
<td><p>會指定是否已擱置的要求。當它已建立<em>Suspend</em>參數搭配使用<strong>New-MailboxRestoreRequest</strong>指令程式可以擱置信箱還原。它可以也被擱置信箱還原作業失敗時是否使用<strong>Suspend-MailboxRestoreRequest</strong>指令程式的管理員。</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>指定要求的識別碼。此 identity 是組合的目標信箱名稱及要求的名稱。</p></td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

執行**Get-MailboxRestoreRequest** cmdlet 以確認您可以檢視信箱還原要求的屬性。如果指令程式會傳回錯誤，請確認您使用正確的語法及身分識別。在某些情況下，此指令程式可能會成功並不會傳回任何結果。例如，如果您已送出與信箱還原要求並執行命令`Get-MailboxRestoreRequest -Status InProgress`會傳回任何結果，然後任一個還原要求目前正在執行。

## 使用命令介面檢視還原統計資料

您可以檢視信箱還原請求的統計資料，您可從資料取得詳細資訊進行疑難排解。

此範例會傳回還原要求 danp\\MailboxRestore1 的預設統計資料。根據預設，傳回的資訊包括名稱、 信箱、 狀態以及完成百分比。

    Get-MailboxRestoreRequestStatistics -Identity danp\MailboxRestore1

此範例會傳回 Dan Park 信箱的統計資料並匯出報告到 .csv 檔案。

    Get-MailboxRestoreRequestStatistics -Identity "Dan Park\MailboxRestore" | Export-CSV \\SERVER01\RestoreRequest_Reports\DanPark_Restorestats.csv

此範例使用 *IncludeReport* 參數傳回有關 Pilar Pinilla 信箱還原請求的額外資訊，並將結果輸入 **Format-List** 指令程式。

    Get-MailboxRestoreRequestStatistics -Identity "Pilar Pinilla\MailboxRestore" -IncludeReport | Format-List 

這個範例會使用 *IncludeReport* 參數，傳回狀態為 `Failed` 之所有還原要求的其他資訊，然後在開始執行命令的位置中，將資訊儲存到 AllRestoreReports.txt 檔案。

    Get-MailboxRestoreRequest -Status Failed | Get-MailboxRestoreRequestStatistics -IncludeReport | Format-List > AllRestoreReports.txt

如需詳細的語法及參數資訊，請參閱 [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/zh-tw/library/ff829912\(v=exchg.150\)) 與 [Get-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829907\(v=exchg.150\))。

## Get-MailboxRestoreRequestStatistics 輸出

根據預設， [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/zh-tw/library/ff829912\(v=exchg.150\))指令程式會傳回要求的要求，目標信箱的別名狀態的名稱和完成百分比。下表列出如果您使用管線處理**Format-List**指令程式指令程式會傳回其他有用的資訊。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>指定要求的名稱。</p></td>
</tr>
<tr class="even">
<td><p><code>Status</code></p></td>
<td><p>指定要求的狀態。</p></td>
</tr>
<tr class="odd">
<td><p><code>StatusDetail</code></p></td>
<td><p>指定要求狀態的相關詳細資訊。例如，如果<code>Status</code>值會傳回<code>InProgress</code>、 <code>StatusDetail</code>值就會傳回<code>InProgress</code>狀態，例如<code>CreatingFolderHierarchy</code>和<code>CopyingMessages</code>的特定階段。</p></td>
</tr>
<tr class="even">
<td><p><code>SyncStage</code></p></td>
<td><p>指定要求在還原處理程序中的進度。</p></td>
</tr>
<tr class="odd">
<td><p><code>Suspend</code></p></td>
<td><p>會指定是否已暫停還原要求。這個值是<code>true</code>在下列情況：</p>
<ul>
<li><p>由於失敗，MRS 已停止或正在停止要求中。</p></li>
<li><p>系統管理員已擱置要求。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SourceExchangeGuid</code></p></td>
<td><p>指定要還原資料之來源信箱的 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><code>SourceRootFolder</code></p></td>
<td><p>指定要從中還原資料的來源信箱階層根資料夾的名稱。如果這個值是空白的會從資料夾上的資訊儲存庫還原資料。</p></td>
</tr>
<tr class="even">
<td><p><code>SourceDatabase</code></p></td>
<td><p>指定來源信箱所在資料庫的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxRestoreFlags</code></p></td>
<td><p>指定要還原的信箱為 <code>Disabled</code> 或 <code>Soft-Deleted</code>。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetAlias</code></p></td>
<td><p>指定目標信箱的別名。</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetIsArchive</code></p></td>
<td><p>指定是否要將信箱還原到封存中。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetExchangeGuid</code></p></td>
<td><p>指定目標信箱的 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetRootFolder</code></p></td>
<td><p>在要還原資料的目標信箱階層中指定之根資料夾名稱。如果這個值是空白的會還原資料的資料夾上的資訊儲存庫。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetDatabase</code></p></td>
<td><p>指定目標信箱所在資料庫的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetMailboxIdentity</code></p></td>
<td><p>指定目標信箱的識別碼。</p></td>
</tr>
<tr class="even">
<td><p><code>IncludeFolders</code></p></td>
<td><p>指定要在還原期間包含資料夾的清單。如果這個值是空白的沒有資料夾所指定時建立要求，並將所有資料夾都還原到信箱 （除非<em>ExcludeFolders</em>參數用來排除特定資料夾中）。</p></td>
</tr>
<tr class="odd">
<td><p><code>ExcludeFolders</code></p></td>
<td><p>指定要在還原期間排除資料夾的清單。如果這個值是空白的沒有資料夾所指定時建立要求，並將所有資料夾都還原到信箱 （除非<em>IncludeFolders</em>參數用來包含特定的資料夾）。</p></td>
</tr>
<tr class="even">
<td><p><code>ExcludeDumpster</code></p></td>
<td><p>指定建立要求時是否排除 [可復原的項目] 資料夾。</p></td>
</tr>
<tr class="odd">
<td><p><code>ConflictResolutionOption</code></p></td>
<td><p>指定目標資料夾和來源資料夾中有相符郵件時，MRS 將採取的動作。</p></td>
</tr>
<tr class="even">
<td><p><code>AssociatedMessagesCopyOption</code></p></td>
<td><p>會指定是否在處理要求時複製相關聯的訊息。相關聯的訊息是特殊包含隱藏的資料與規則、 檢視及表單的相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><code>BadItemLimit</code></p></td>
<td><p>指定要求遭遇損毀郵件時，MRS 要略過的錯誤項目數量。</p></td>
</tr>
<tr class="even">
<td><p><code>BadItemsEncountered</code></p></td>
<td><p>指定命令發生損毀的郵件數目。如果<em>BadItemsEncountered</em>值大於<em>BadItemLimit</em>值，要求就會失敗。</p></td>
</tr>
<tr class="odd">
<td><p><code>QueuedTimeStamp</code></p></td>
<td><p>指定要求初始化至 MRS 的日期和時間。</p></td>
</tr>
<tr class="even">
<td><p><code>StartTimeStamp</code></p></td>
<td><p>指定 MRS 開始處理還原請求的日期與時間。</p></td>
</tr>
<tr class="odd">
<td><p><code>LastUpdateTimeStamp</code></p></td>
<td><p>指定的日期和時間的要求進行最後變更。變更可能會對由系統管理員或 MRS。</p></td>
</tr>
<tr class="even">
<td><p><code>SuspendTimeStamp</code></p></td>
<td><p>指定擱置要求的日期和時間。</p></td>
</tr>
<tr class="odd">
<td><p><code>OverallDuration</code></p></td>
<td><p>會指定完成要求所花的時間量。<code>Failed</code>狀態要求時，此值會指定要啟動的要求及要求失敗之間的時間量。如果要求不完整，這個值會指定之間所起始的要求及<strong>Get-MailboxRestoreRequestStatistics</strong> cmdlet 所執行的時間量。</p></td>
</tr>
<tr class="even">
<td><p><code>TotalSuspendedDuration</code></p></td>
<td><p>指定要求處於 <code>Suspended</code> 狀態的時間長度。</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalFailedDuration</code></p></td>
<td><p>指定要求處於 <code>Failed</code> 狀態的時間長度。</p></td>
</tr>
<tr class="even">
<td><p><code>TotalQueuedDuration</code></p></td>
<td><p>指定要求處於 <code>Queued</code> 狀態的時間長度。</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalInProgressDuration</code></p></td>
<td><p>指定要求處於 <code>In Progress</code> 狀態的時間長度。</p></td>
</tr>
<tr class="even">
<td><p><code>TotalStalledDueToHADuration</code></p></td>
<td><p>指定要求因為高可用性而延遲的時間長度。</p></td>
</tr>
<tr class="odd">
<td><p><code>MRSServerName</code></p></td>
<td><p>指定處理要求的 Client Access Server 名稱。</p></td>
</tr>
<tr class="even">
<td><p><code>EstimatedTransferSize</code></p></td>
<td><p>指定還原的總檔案大小，或是請求處於 <code>In Progress</code> 狀態，MRS 預期還原的檔案大小。</p></td>
</tr>
<tr class="odd">
<td><p><code>EstimatedTransferItemCount</code></p></td>
<td><p>指定要求處於 <code>In Progress</code> 狀態時已還原的項目數量，或 MRS 預期要還原的項目數量。</p></td>
</tr>
<tr class="even">
<td><p><code>BytesTransferredPerMinute</code></p></td>
<td><p>指定每分鐘所傳輸位元組的平均數量。</p></td>
</tr>
<tr class="odd">
<td><p><code>ItemsTransferred</code></p></td>
<td><p>指定所傳輸項目的數量。</p></td>
</tr>
<tr class="even">
<td><p><code>PercentComplete</code></p></td>
<td><p>指定已完成要求的百分比。</p></td>
</tr>
<tr class="odd">
<td><p><code>CompletedRequestAgeLimit</code></p></td>
<td><p>指定是否將多久完成的還原要求會在刪除之前會保留。預設值為 30 天。</p></td>
</tr>
<tr class="even">
<td><p><code>PositionInQueue</code></p></td>
<td><p>如果要求尚未開始，則這個值會指定佇列中要求的位置。</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureCode</code></p></td>
<td><p>如果發生失敗，這個值會指定錯誤碼。</p></td>
</tr>
<tr class="even">
<td><p><code>FailureType</code></p></td>
<td><p>如果發生失敗，這個值會指定失敗類型。</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureSide</code></p></td>
<td><p>如果發生失敗，這個值會指定失敗是在目標信箱還是來源信箱上發生。</p></td>
</tr>
<tr class="even">
<td><p><code>Message</code></p></td>
<td><p>如果沒有失敗，這個值會指定失敗訊息。這個值也可以指定擱置註解。</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureTimestamp</code></p></td>
<td><p>如果要求失敗，則此值會指出要求失敗的日期和時間。</p></td>
</tr>
<tr class="even">
<td><p><code>FailureContext</code></p></td>
<td><p>如果要求失敗，這個值會指定失敗時正在執行之動作的相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><code>ValidationMessage</code></p></td>
<td><p>如果要求無效，這個值會指定原因。</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>指定 MRS 在哪個資料庫上儲存要求的詳細狀態。</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>指定要求的識別碼。</p></td>
</tr>
<tr class="even">
<td><p><code>Report</code></p></td>
<td><p>如果使用 <em>IncludeReport</em> 參數，這個值會指定可用於疑難排解要求的資訊。</p></td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

執行**Get-MailboxRestoreRequestStatistics** cmdlet 以確認您可以檢視信箱還原要求的統計資料。如果指令程式會傳回錯誤，請確認您使用正確的身分識別的還原要求。

## 使用命令介面以變更還原請求屬性

如果信箱還原請求失敗，您可以使用 **Set-MailboxRestoreRequest** 指令程式以變更請求的屬性以嘗試從失敗復原。

此範例指定 Debra Garcia 的信箱之還原請求 MailboxRestore1 略過 10 個損壞信箱項目。

    Set-MailboxRestoreRequest -Identity "Debra Garcia\MailboxRestore1" -BadItemLimit 10

本範例會指定 Florence Flipo 信箱還原要求 MailboxRestore1 會略過 100 個損毀的項目。因為*BadItemLimit*值大於 50，必須指定*AcceptLargeDataLoss*參數。

    Set-MailboxRestoreRequest -Identity "Florence Flipo\MailboxRestore1" -BadItemLimit 100 -AcceptLargeDataLoss

如需詳細的語法及參數資訊，請參閱 [Set-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829909\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功變更在還原要求的內容，請執行**Get-MailboxRestoreRequestStatistics**指令程式來顯示的還原要求的修訂的內容。如果已成功建立的還原要求， *Status*屬性都有`Queued`、 `InProgress`或`Completed`的值。完成的還原要求後，虛刪除信箱的內容會出現在目標信箱。

如需詳細的語法及參數資訊，請參閱 [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/zh-tw/library/ff829912\(v=exchg.150\))。

## 使用命令介面來擱置還原要求

建立要求，但還要求達到的`Completed`狀態您可以暫停指定在還原要求隨時。若要繼續使用[Resume-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829908\(v=exchg.150\))指令程式的還原要求的命令語法本主題稍後的請參閱使用命令介面\] 以繼續還原要求。

此範例暫停 Pilar Pinilla 信箱的還原請求 MailboxRestore1。

    Suspend-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

此範例藉由先擷取狀態為 `InProgress` 的所有還原請求，然後輸入結果至 **Suspend-MailboxRestoreRequest** 指令程式並包括暫停指令「Resume after FY13Q2 Maintenance」以暫停進行中的所有還原請求。

    Get-MailboxRestoreRequest -Status InProgress | Suspend-MailboxRestoreRequest -SuspendComment "Resume after FY13Q2 Maintenance"

如需詳細的語法及參數資訊，請參閱 [Suspend-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829906\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功暫停信箱還原請求，執行下列指令。

    Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status

*Suspend*屬性的值等於`True`，已成功擱置的還原要求。此外， `Suspended`*Status*屬性的值會指出已暫停還原要求。

## 使用命令介面來繼續執行還原要求

使用 **Resume-MailboxRestoreRequest** 指令程式以繼續失敗或暫停的還原請求。

此範例會繼續還原請求 Pinilla\\MailboxRestore1。

    Resume-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

此範例會繼續狀態為「失敗」的所有還原請求。

    Get-MailboxRestoreRequest -Status Failed | Resume-MailboxRestoreRequest

如需詳細的語法及參數資訊，請參閱 [Resume-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829908\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證已繼續還原請求，執行下列指令。

    Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status

如果*Suspend*屬性的值等於`False`，成功繼續還原要求。此外， `InProgress`*Status*屬性的值會指出的還原要求繼續。

## 使用命令介面來移除還原要求

您可以使用**Remove-MailboxRestoreRequest**指令程式來移除信箱還原要求。如果您移除在還原要求信箱資料一開始會複製到目標信箱之後，複製到信箱資料仍會保留在目標信箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如先前所述，已完成的還原請求會根據預設保留 30 天再自動刪除。</td>
</tr>
</tbody>
</table>


此範例會移除還原請求 Pilar Pinilla\\MailboxRestore1。

    Remove-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

這個範例會移除狀態為「已完成」的所有還原要求。

    Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest

本範例會使用 MBXDB01 上儲存要求*RequestGuid*參數來取消的還原要求。需要的*RequestGuid*和*RequestQueue*參數的參數組只能用於偵錯用途的 Microsoft 複寫服務。您應該使用只有在 Microsoft 客戶服務與支援部門另有指示將此參數。

    Remove-MailboxRestoreRequest -RequestQueue MBXDB01 -RequestGuid 25e0eaf2-6cc2-4353-b83e-5cb7b72d441f

如需詳細的語法及參數資訊，請參閱 [Remove-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829910\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功移除信箱還原請求，執行下列指令。

    Get-MailboxRestoreRequest -Identity <identity of removed restore request>

指令會傳回錯誤，指出還原請求不存在。

您也可以執行**Get-MailboxRestoreRequest**指令程式。如果在還原要求已成功移除，它不會包含在結果中。

