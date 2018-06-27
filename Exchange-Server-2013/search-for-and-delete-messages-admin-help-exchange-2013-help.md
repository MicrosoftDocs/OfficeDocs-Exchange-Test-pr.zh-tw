---
title: '搜尋並刪除郵件 - 管理中心說明: Exchange Online Help'
TOCTitle: 搜尋並刪除郵件 - 管理中心說明
ms:assetid: 8c36bb03-e716-4fdd-9958-4aa7a2a1db42
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff459253(v=EXCHG.150)
ms:contentKeyID: 52062351
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 搜尋並刪除郵件 - 管理中心說明

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-12-20_

系統管理員可以使用 **Search-Mailbox** Cmdlet 來搜尋使用者信箱，然後刪除信箱中的郵件。

若要以單一步驟搜尋並刪除郵件，請執行包含 *DeleteContent* 參數的 **Search-Mailbox** 指令程式。不過，當您這麼做時，無法預覽搜尋結果或產生將由搜尋傳回的郵件記錄，而且您可能會不慎刪除一些郵件。若要在刪除郵件之前預覽在搜尋中找到的郵件記錄，請執行包含 *LogOnly* 參數的 **Search-Mailbox** 指令程式。

您可以使用 *TargetMailbox* 和 *TargetFolder* 參數，將郵件複製到其他信箱，做為另一層保護。如此可以保留已刪除郵件的副本，以防您需要再次存取這些郵件。

## 開始前需要瞭解什麼？

  - 預估完成時間：10 分鐘。實際時間可能視信箱大小和搜尋查詢而有所不同。

  - 您不能使用 Exchange 管理中心 (EAC) 執行這些程序。您必須使用命令介面。

  - 您必須同時被指派下列管理角色，才能在使用者的信箱中搜尋並刪除郵件：
    
      - **信箱搜尋：**這個角色可讓您在組織中的多個信箱之間搜尋郵件。根據預設，系統管理員不會被指派這個角色。若要指派此角色給自己以便搜尋信箱，請將您自己增加為「探索管理」角色群組的成員。請參閱[Exchange 中指派 eDiscovery 權限](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)。
    
      - **信箱匯入匯出：**這個角色可讓您從使用者的信箱中刪除郵件。依預設，此角色不會指派給任何角色群組。若要從使用者的信箱中刪除郵件，您可以將信箱匯入匯出角色新增至組織管理角色群組。如需詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)中的＜Add a role to a role group＞。

  - 如果您要從中刪除郵件的信箱已啟用單一項目復原，則必須先停用該功能。如需詳細資訊，請參閱[啟用或停用單一項目復原的信箱](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md)。

  - 如果您要從中刪除郵件的信箱處於保留狀態，建議您先與記錄管理或法務部門確認，然後再移除保留並刪除信箱內容。獲得核准之後，請依照[清除 \[可復原的項目\] 資料夾](clean-up-the-recoverable-items-folder-exchange-2013-help.md)主題中所列的步驟進行。

  - 您可以使用 **Search-Mailbox** Cmdlet 來搜尋信箱，上限為 10,000 個。如果您是 Exchange Online 組織，且擁有超過 10,000 個信箱，則可以使用「規範搜尋」功能 (或對應的 **New-ComplianceSearch** Cmdlet) 來搜尋信箱，且數量不受限制。接著您可以使用 **New-ComplianceSearchAction** Cmdlet 來刪除規範搜尋所傳回的郵件。如需詳細資訊，請參閱[搜尋並刪除您的 Office 365 組織中的電子郵件訊息](https://go.microsoft.com/fwlink/p/?linkid=786856)。

  - 如果您納入搜尋查詢 (藉由使用 *SearchQuery* 參數)，則 **Search-Mailbox** Cmdlet 會在搜尋結果中傳回上限為 10,000 個的項目。因此，如果您納入搜尋查詢，則可能需要執行 **Search-Mailbox** 命令數次，才能刪除 10,000 個以上的項目。

  - 當您執行**Search-Mailbox**指令程式也要搜尋使用者的封存信箱。同樣地，主要的封存信箱中的項目將會被刪除時**Search-Mailbox**指令程式搭配*DeleteContent*參數。若要避免此問題，您可以包含*DoNotIncludeArchive*參數。 此外，我們建議您不要使用*DeleteContent*交換器刪除已自動展開封存啟用因為可能會發生未預期的資料遺失的Exchange Online信箱中的郵件。

## 搜尋郵件並記錄搜尋結果

此範例會搜尋 April Stewart 的信箱中 \[主旨\] 欄位中包含 "Your bank statement" 字詞的郵件，並將搜尋結果記錄在系統管理員信箱的 SearchAndDeleteLog 資料夾中。不會將郵件複製到目標信箱或從中刪除。

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

此範例會在組織的所有信箱中搜尋檔名中含有 "Trojan" 一字之任何附加檔案類型的郵件，並傳送一則記錄檔訊息到系統管理員的信箱。

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery attachment:trojan* -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

如需詳細的語法及參數資訊，請參閱 [Search-Mailbox](https://technet.microsoft.com/zh-tw/library/dd298173\(v=exchg.150\))。

回到頁首

## 搜尋和刪除郵件

此範例會搜尋 April Stewart 的信箱中 \[主旨\] 欄位中包含 "Your bank statement" 字詞的郵件，並從來源信箱刪除這些郵件，而不將搜尋結果複製到其他資料夾。如先前所述，您必須取得「信箱匯入匯出」管理角色，才能刪除使用者信箱中的郵件。 。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您使用包含 <em>DeleteContent</em> 參數的 <strong>Search-Mailbox</strong> 指令程式時，郵件會從來源信箱永久刪除。在您永久刪除郵件之前，建議您使用 <em>LogOnly</em> 參數產生在搜尋中找到之郵件的記錄，然後再進行刪除，或者在從來源信箱刪除郵件時，先將這些郵件複製到其他信箱。</td>
</tr>
</tbody>
</table>


    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -DeleteContent

此範例會搜尋 April Stewart 的信箱中 \[主旨\] 欄位中包含 "Your bank statement" 字詞的郵件、將搜尋結果複製到 BackupMailbox 信箱的 AprilStewart-DeletedMessages 資料夾中，然後再從 April 的信箱刪除郵件。

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox "BackupMailbox" -TargetFolder "AprilStewart-DeletedMessages" -LogLevel Full -DeleteContent

此範例會在組織的所有信箱中搜尋主旨行是 "Download this file" 的郵件，然後永久刪除這些郵件。

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery 'Subject:"Download this file"' -DeleteContent

如需詳細的語法及參數資訊，請參閱 [Search-Mailbox](https://technet.microsoft.com/zh-tw/library/dd298173\(v=exchg.150\))。

回到頁首

## 使用 -LogLevel Full 參數

在前面的部分範例中，*LogLevel* 參數會搭配 `Full` 值一起用來記錄 **Search-Mailbox** Cmdlet 所傳回之結果的詳細資訊。 當您納入此參數時，系統會建立電子郵件訊息，並傳送到 *TargetMailbox* 參數所指定的信箱。記錄檔 (CSV 格式，且名稱為 Search Results.csv 的檔案) 會附加到此電子郵件訊息，並存放在 *TargetFolder* 參數所指定的資料夾中。當您執行 **Search-Mailbox** Cmdlet 時，記錄檔會在搜尋結果所含的每封郵件中包含一個資料列。

