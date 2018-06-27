---
title: '信箱匯入及匯出要求: Exchange 2013 Help'
TOCTitle: 信箱匯入及匯出要求
ms:assetid: 157a7d88-d3aa-4056-9a50-df67451b14be
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633455(v=EXCHG.150)
ms:contentKeyID: 50472672
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 信箱匯入及匯出要求

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

使用**MailboxImportRequest**或**MailboxExportRequest**指令程式會將 Exchange 管理命令介面中，您可以匯入的資料或將資料匯出至.pst 檔案。在啟動信箱匯入或匯出要求之後，程序是由Microsoft Exchange信箱複寫服務 (MRS) 以非同步方式完成。MRS 存在於所有Exchange 2010用戶端存取伺服器上，而且是負責移動信箱並匯入及匯出.pst 檔案的服務。

**目錄**

Reasons to import or export mailbox data

Advantages to using import and export requests

Considerations

Importing mailbox data

Exporting mailbox data

## 匯入或匯出信箱資料的原因

下列原因可能讓您想匯入或匯出信箱資料：

  - **符合規範需求**  您可以將信箱內容匯出至.pst 檔案供法律調查使用。匯出完成之後，您可以匯入特別針對規範用途使用信箱的內容。

  - **建立信箱時間點快照** 在建立特定信箱的快照後，您就不需要保留信箱資料庫的整個備份集。

  - **移至他或其信箱或個人封存的使用者的.pst 檔案**  Microsoft Outlook使用者可以在本機儲存的電子郵件為.pst 檔案。使用[New-MailboxImportRequest](https://technet.microsoft.com/zh-tw/library/ff607310\(v=exchg.150\))指令程式，您可以將資料從使用者的.pst 檔案移至他或其信箱或個人封存。這是從使用者的本機電腦的電子郵件傳送到Exchange伺服器的簡易方法。

## 使用匯入和匯出要求的優點

在Exchange 2013 使用匯入及匯出要求包含下列優勢：

  - .pst 提供者會包含在可讀取及寫入 .pst 檔案的 Exchange 2013 中。

  - 匯出及匯入要求的非同步。程序是由 MRS、 佇列和節流 framework 利用執行。

  - .pst 檔案可直接匯入使用者的個人封存。

  - 可同時匯入或匯出多個 .pst 檔案。

  - .pst 檔案可位於 Exchange 伺服器可存取的任何共用網路磁碟機上。

  - Exchange 2013支援這些.pst 檔案 ︰ Office Outlook 2007和Outlook 2010所建立的 Unicode 檔案

## 附註

匯入或匯出信箱資料之前，請考慮下列事項：

  - 若要匯入或匯出信箱資料，可供您Exchange伺服器存取的網路共用的資料夾必須設定。您必須也授與讀取/寫入權限Exchange受信任子系統群組使群組可以存取您匯入及匯出信箱資料的網路共用。如果您沒有授與此權限，您會收到錯誤訊息表示該Exchange無法建立連線的目標信箱。

  - Outlook所支援的最大的.pst 檔案大小為 50 gb。因此，我們建議您不要大於 50 GB 的.pst 檔案匯入。您可以建立多個信箱的.pst 檔案大於 50 GB，指定以包含或排除特定資料夾或使用內容篩選器。

  - 匯出及匯入要求被執行 MRS、 程序也移動要求和信箱還原要求。所有要求排入佇列，會由 MRS 節流處理。

  - 視檔案大小、網路頻寬和 MRS 節流而定，匯入和匯出信箱資料可能需要數小時。

  - 資料不能匯入至公用資料夾或公用資料夾資料庫。

## 匯入信箱資料

使用**MailboxImportRequest**指令程式將資料從.pst 檔案匯入至信箱或個人封存。以下是您可以指定從.pst 檔案匯入信箱資料時的選項清單：

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>匯入資料的信箱必須存在。您不能沒有信箱的使用者帳戶來匯入資料。</td>
</tr>
</tbody>
</table>


  - 您可以比一個從中它已匯出為不同的使用者帳戶來匯入資料。例如，您可以從 john@contoso.com 匯出資料並匯入 legaldiscovery@contoso.com。

  - 您可以指定 *IsArchive* 參數，使項目只能匯入使用者的個人封存。

  - 如果相關聯的資料夾的郵件中的.pst 檔案，您就可以將其使用*AssociatedMessagesCopyOption*參數匯入。相關聯的訊息包含隱藏的資料與規則、 檢視及表單的相關資訊。若存在.pst 檔案中，會匯入從 safety net 的所有郵件。

  - 您可以使用 *IncludeFolders* 或 *ExcludeFolders* 參數以包含或排除特定資料夾。

  - 您可以排除使用*ExcludeDumpster*參數的可復原的項目\] 資料夾。根據預設，匯入要求包含使用者的 \[可復原的項目\] 資料夾中的.pst 檔案時。

## 信箱匯入要求指令程式

針對信箱匯入要求使用下列指令程式。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>指令程式</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607310(v=exchg.150)">New-MailboxImportRequest</a></p></td>
<td><p>啟動匯入至信箱或個人封存的.pst 檔案的程序。您可以建立每個信箱的多個匯入要求。每次要求必須具有唯一的名稱。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607317(v=exchg.150)">Set-MailboxImportRequest</a></p></td>
<td><p>建立要求或復原失敗要求之後變更匯入要求選項。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607309(v=exchg.150)">Suspend-MailboxImportRequest</a></p></td>
<td><p>建立要求後並在要求達到 [已完成] 狀態前，隨時可擱置匯入要求。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607306(v=exchg.150)">Resume-MailboxImportRequest</a></p></td>
<td><p>繼續已擱置或失敗的匯入要求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607311(v=exchg.150)">Remove-MailboxImportRequest</a></p></td>
<td><p>會移除完全或部分完成匯入要求。完成匯入要求不會自動清除。您必須使用此指令程式加以移除。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607368(v=exchg.150)">Get-MailboxImportRequest</a></p></td>
<td><p>檢視與匯入要求有關的一般資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607315(v=exchg.150)">Get-MailboxImportRequestStatistics</a></p></td>
<td><p>檢視與匯入要求有關的詳細資訊。</p></td>
</tr>
</tbody>
</table>


## 匯出信箱資料

使用**MailboxExportRequest**指令程式設定為將信箱資料匯出至.pst 檔案。您可以匯出一個信箱或數個信箱，但是只有一個要求每次寫入至每個.pst 檔案。以下是您可以指定信箱資料匯出至.pst 檔案時的選項清單：

  - 您可以使用 *IsArchive* 參數匯出個人封存資料。

  - 您可以篩選使用*ContentFilter*參數都要匯出的郵件。您可以篩選郵件內容、 attachment、 寄件者、 收件者、 收件匣類別、 重要性、 郵件類型、 郵件大小及傳送郵件時接收到，或過期。

  - 您可以指定以包含或排除使用*IncludeFolders*或*ExcludeFolders*參數的資料夾。如果從Exchange 2013信箱匯出資料，您也可以排除使用*ExcludeDumpster*參數的可復原的項目\] 資料夾。

  - 您可以將匯出使用*AssociatedMessagesCopyOption*參數相關聯的訊息。相關聯的訊息包含隱藏的資料與規則、 檢視及表單的相關資訊。根據預設，相關的項目不複製至.pst 檔案。

## 信箱匯出要求指令程式

針對信箱匯出要求使用下列指令程式。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>指令程式</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607299(v=exchg.150)">New-MailboxExportRequest</a></p></td>
<td><p>啟動從主要信箱或個人封存的資料匯出至.pst 檔案的程序。您可以建立多個匯出要求每個信箱。每次要求必須具有唯一的名稱。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607312(v=exchg.150)">Set-MailboxExportRequest</a></p></td>
<td><p>建立要求或復原失敗要求之後變更匯出要求選項。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607305(v=exchg.150)">Suspend-MailboxExportRequest</a></p></td>
<td><p>建立要求後並在要求達到 [已完成] 狀態前，隨時可擱置匯出要求。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607476(v=exchg.150)">Resume-MailboxExportRequest</a></p></td>
<td><p>繼續已擱置或失敗的匯出要求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607464(v=exchg.150)">Remove-MailboxExportRequest</a></p></td>
<td><p>會移除完全或部分完成的匯出要求。完成的匯出要求不會自動清除。您必須使用此指令程式加以移除。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607479(v=exchg.150)">Get-MailboxExportRequest</a></p></td>
<td><p>檢視與匯出要求有關的一般資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/ff607316(v=exchg.150)">Get-MailboxExportRequestStatistics</a></p></td>
<td><p>檢視與匯出要求有關的詳細資訊。</p></td>
</tr>
</tbody>
</table>

