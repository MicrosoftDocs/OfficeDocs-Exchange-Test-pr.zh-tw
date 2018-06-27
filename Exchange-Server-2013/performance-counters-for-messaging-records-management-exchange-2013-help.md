---
title: '通訊記錄管理的效能計數器: Exchange 2013 Help'
TOCTitle: 通訊記錄管理的效能計數器
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 51409237
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通訊記錄管理的效能計數器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

本主題中的效能計數器監視受管理的資料夾助理員它實作的 Microsoft Exchange Server 2010通訊的記錄管理 (MRM)。因為執行受管理的資料夾助理員會大量消耗資源的程序，您應只有在您的伺服器可以容忍的額外負載時加以執行。您也應該監視伺服器效能受管理的資料夾助理員執行時。除了本主題中所列的效能計數器，您可能也要監視監視項目如磁碟效能及 CPU 使用率的其他效能計數器。

如需監視已執行 MRM 之電腦的詳細資訊，請參閱[監視通訊記錄管理](monitoring-messaging-records-management-exchange-2013-help.md)。

## MRM 的效能計數器

下表描述 MRM 的效能計數器。

### 效能計數器、效能物件及描述

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>效能計數器</th>
<th>效能物件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>平均信箱處理時間 (以秒為單位)</p></td>
<td><p>MSExchange 助理員</p></td>
<td><p>計算以時間為基礎的助理員其信箱平均處理時間。</p></td>
</tr>
<tr class="even">
<td><p>Mailboxes Processed</p></td>
<td><p>MSExchange 助理員</p></td>
<td><p>計算自服務啟動以來，以時間為基礎的助理員已處理的信箱數。</p></td>
</tr>
<tr class="odd">
<td><p>Mailboxes processed/sec</p></td>
<td><p>MSExchange 助理員</p></td>
<td><p>判斷以時間為基礎的助理員每秒處理信箱的速率。</p></td>
</tr>
<tr class="even">
<td><p>Items Deleted but Recoverable</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>計算自之最新的排程間隔開始刪除的受管理的資料夾助理員的項目數。（會透過 [可復原的項目] 資料夾仍可復原的項目）。數排定期間的排程間隔和任何您指定進行處理的信箱中的項目處理的信箱中包含的項目。此計數器會重設為零開頭的每個排程間隔。</p></td>
</tr>
<tr class="odd">
<td><p>Items Journaled</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>計算的最新的排程間隔開始自日誌的受管理的資料夾助理員的項目數。數排定期間的目前工作週期與所指定的處理任何信箱中的項目處理的信箱中包含的項目。此計數器會重設為零開頭的每個工作週期。</p></td>
</tr>
<tr class="even">
<td><p>Items Marked as Past Retention Date</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>會統計標示為超過其保留日期的受管理的資料夾助理員自之最新的排程間隔開始的項目數。數信箱排程處理期間的排程間隔與所指定的處理任何信箱中的項目中包含的項目。此計數器會重設為零開頭的每個排程間隔。</p></td>
</tr>
<tr class="odd">
<td><p>Items Moved</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>會統計之後的最新的排程間隔的起點移動的受管理的資料夾助理員的項目數。數排定期間的排程間隔與所指定的處理任何信箱中的項目處理的信箱中包含的項目。此計數器會重設為零開頭的每個排程間隔。</p></td>
</tr>
<tr class="even">
<td><p>Items Permanently Deleted</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>會統計永久刪除的受管理的資料夾助理員自開頭的最新的排程間隔的項目數。數排定期間的排程間隔與所指定的處理任何信箱中的項目處理的信箱中包含的項目。此計數器會重設為零的每個排程間隔開頭。</p></td>
</tr>
<tr class="odd">
<td><p>Items Subject to Retention Policy</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>自之最新的排程間隔開始計算受限於受管理的資料夾助理員的保留原則的項目數。數排定期間的排程間隔與所指定的處理任何信箱中的項目處理的信箱中包含的項目。此計數器會重設為零開頭的每個排程間隔。此計數器會是下列四種項到期相關的計數器的總和：</p>
<ul>
<li><p>Items Journaled</p></li>
<li><p>Items Marked as Past Retention Date</p></li>
<li><p>Items Moved</p></li>
<li><p>Items Permanently Deleted</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsExpired - 受保留原則限制之項目的大小 (以位元組為單位)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出由受管理的資料夾助理員終止 (SoftDelete、HardDelete、MoveToArchive) 之項目的總大小。</p>
<p>包括下列項目：</p>
<ul>
<li><p>依據受管理的資料夾信箱原則遭到刪除或移至受管理的自訂資料夾的郵件</p></li>
<li><p>依據使用者的保留原則遭到刪除或移至封存的郵件</p></li>
<li><p>依據暫放原則終止的郵件</p></li>
<li><p>依據系統清理標記清理的郵件</p></li>
</ul>
<p>此計數器會在受管理的資料夾助理員工作週期的每個工作週期檢查點重設為零。</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsSoftDeleted - 已刪除但可以復原之項目的大小 (以位元組為單位)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出由受管理的資料夾助理員虛刪除之項目的總大小。</p>
<p>包括下列項目：</p>
<ul>
<li><p>依據受管理的資料夾信箱原則虛刪除的郵件</p></li>
<li><p>依據保留原則虛刪除的郵件</p></li>
</ul>
<p>此計數器會在受管理的資料夾助理員工作週期的每個工作週期檢查點重設為零。</p></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsPermanentlyDeleted - 永久刪除之項目的大小 (以位元組為單位)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出由受管理的資料夾助理員虛刪除之項目的總大小。</p>
<p>包括下列項目：</p>
<ul>
<li><p>依據受管理的資料夾信箱原則實刪除的郵件</p></li>
<li><p>依據保留原則實刪除的郵件</p></li>
<li><p>依據可復原的項目原則實刪除的郵件</p></li>
</ul>
<p>此計數器會在受管理的資料夾助理員工作週期的每個工作週期檢查點重設為零。</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsMoved - 由於封存原則標記移動之項目的大小 (以位元組為單位)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出由受管理的資料夾助理員移至資料夾或封存之項目的總大小。</p>
<p>包括下列項目：</p>
<ul>
<li><p>依據受管理的資料夾信箱原則移至受管理的自訂資料夾的郵件</p></li>
<li><p>依據保留原則移至個人封存的郵件</p></li>
</ul>
<p>此計數器會在受管理的資料夾助理員工作週期的每個工作週期檢查點重設為零。</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsWithPersonalTag - 加上個人標記 (到期或封存) 戳記的項目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出使用者使用個人標記來標記項目的次數。</p>
<p>這包括刪除和封存標記。</p>
<p>例如：</p>
<ul>
<li><p>使用個人標記來標記某個項目。</p></li>
<li><p>使用另一個個人標記來重新標記具有個人標記的項目。</p></li>
</ul>
<p>如果使用個人標記來標記資料夾，則計數器會依據資料夾中的項目總數來遞增。</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsWithDefaultTag - 加上預設標記 (到期或封存) 戳記的項目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出根據使用者動作而被指派預設原則標記 (DPT) 的項目數，例如，當使用者選取具有個人標記的郵件且選取 <strong>[使用資料夾原則]</strong> 時。</p>
<p>如果將具 DPT 的保留原則指派給新使用者，則計數器會依據由於保留原則而被指派 DPT 的項目數來遞增。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果使用者擁有具 DPT 的保留原則，則透過傳輸送達的新郵件會取得預設標記，且不會由此計數器追蹤。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>TotalItemsWithSystemCleanupTag - 加上系統清理標記戳記的項目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>會指出標記了系統清理標籤的項目數。這包括隱藏的使用者信箱的中繼資料項目。</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsExpiredByDefaultExpiryTag - 由於預設到期標記而過期的項目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出由於保留原則中任何非個人 (預設或系統) 標記，而由受管理的資料夾助理員終止 (虛刪除或硬刪除) 的項目數。</p>
<p>這不包含由 [可復原的項目] 清理或系統清理所終止的項目。</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsExpiredByPersonalExpiryTag - 由於個人到期標記而過期的項目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出由於保留原則中的個人標記，而由受管理的資料夾助理員終止 (虛刪除或實刪除) 的項目數。</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsMovedByDefaultArchiveTag - 由於預設封存標記而移動的項目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出由於保留原則中任何非個人 (預設或系統) 封存標記，而由受管理的資料夾助理員移至封存的項目數。</p>
<p>這不包含由 [可復原的項目] 清理移至封存中 [可復原的項目] 資料夾內的項目。</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsMovedByPersonalArchiveTag - 由於封存標記而移動的項目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出由於保留原則中的個人封存標記，而由受管理的資料夾助理員移至封存的項目數。</p></td>
</tr>
<tr class="odd">
<td><p>TotalMovedDumpsterItems - 信箱暫放移動的項目</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>指出由 [可復原的項目] 清理移至封存中 [可復原的項目] 資料夾內的項目數。</p></td>
</tr>
</tbody>
</table>

